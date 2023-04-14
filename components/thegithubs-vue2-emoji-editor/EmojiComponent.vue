<template>
  <view class="emoji" style="width:60vw;max-width:60vw;min-width:60vw">
  	<view class="teatarea">
  		<view class="field">
  			<view
					id="contenteditable"
					:class="{wordLimit: max === 0 || !showWordLimit, forbid: forbid}"
					:style="`${editorStyle}; border: ${isFocus ? borderActive : border};`"
					:contenteditable="canEdit"
					:placeholder="placeholder"
					@compositionstart="typing = true"
					@compositionend="typing = false"
					@keyup="enter"
					@keydown="keydown"
					@input="input"
					@click="enter"
					@focus="focus"
					@blur="blur"
				></view>
  			
  		
  		</view>
  	</view>
  </view>
</template>

<script>
export default {
  name: 'EmojiComponent',
	model: {
		prop: 'value',
		event: 'change'
	},
  props: {
		disabled: { //是否禁用
			type: Boolean,
			default: false
		},
    showWordLimit: { //是否显示输入字数统计 max等于0则不显示
    	type: Boolean,
    	default: true
    },
    clearable: { //是否可清空
    	type: Boolean,
    	default: true
    },
    max: { //可输入的最大长度 等于0则不限制
    	type: Number,
    	default: 0
    },
    placeholder: { //占位符
    	type: String,
    	default: '请输入...'
    },
    value: { //绑定值
    	type: String,
    	default: ''
    },
    autofocus: { //是否自动聚焦
    	type: Boolean,
    	default: true
    },
		editorStyle: { //输入框样式
			type: String,
			default: ''
		},
		border: { //默认边框
			type: String,
			default: '1px solid #f6f7f8'
		},
		borderActive: { //激活时边框
			type: String,
			default: '1px solid #f6f7f8'
		},
		imgStyle: { //输入框图片样式
			type: String,
			default: 'max-width: 90px;'
		}
  },
	data(){
		return {
			content: '',
			startOffset: 0,
			range: null,
			total: 0,
			typing: false, //输入状态
			canEdit: this.disabled ? false : 'plaintext-only',
			isFocus: false,
			forbid: false,
		}
	},
	mounted(){
		this.init()
	},
	watch: {
		content(){
			this.$emit('change', this.getContent(), this.total)
		}
	},
	inheritAttrs: false,
	methods: {
		lineFeed(h){
			//输出换行符，图片<img 去掉js事件 如onclick等
			return h.indexOf('<img') > -1 ? h.replace(/[\r\n]/g, '<br>').replace(/on.+?=".*?"/i, '') : h
		},
		init(){
			//初始化
			let $content = document.querySelector('#contenteditable'),
				range = this.range,
				selection = getSelection()
			this.content = this.value
			$content.innerHTML = this.content
			if (this.autofocus) this.focus()
			if (!this.disabled) {
				if (!this.autofocus) return
				range = selection.getRangeAt(0)
				range.selectNodeContents($content)
				range.collapse(false)
				selection.removeAllRanges()
				selection.addRange(range)
			}
			this.calc()
		},
		getContent(){
			//获取内容 非img转义< &lt; > &gt;
			return this.lineFeed(this.content.replace(/<((?!img).+?)>/g, ($1, $2) => `&lt;${$2}&gt;`).trim())
		},
		modelValue(){
			this.content += ''
		},
		focus(e){
			if (this.isFocus) return
			this.isFocus = true
	 		document.querySelector('#contenteditable').focus()
			if (e && e.sourceCapabilities) this.$emit('focus', e)
		},
		blur(e){
			this.isFocus = false
			if (e && !e.relatedTarget) this.$emit('blur', e)
		},
		clear(){
			//清空内容 重置
			this.content = ''
			this.total = 0
			this.startOffset = 0
			document.querySelector('#contenteditable').innerHTML = ''
			this.focus()
			this.$emit('clear')
		},
		keydown(e){
			//达到最大字数时，除了删除shift方向ctrl键，其他不可用
			const key = e.keyCode || e.which
			if (this.max !== 0 && this.total >= this.max) {
				if ((!e.ctrlKey && (key != 67 || key != 86)) && key != 8 && key != 46 && key != 16 && key != 37 && key != 38 && key != 39 && key != 40) {
					this.canEdit = false
					this.forbid = true
					setTimeout(() => {
						this.canEdit = 'plaintext-only'
						this.forbid = false
					}, 50)
				}
			}
		},
		calc(){
			//计算长度
			const $content = document.querySelector('#contenteditable')
			let emojiTimes = 0
			for (let i = 0; i < $content.childNodes.length; i++) {
				const { nodeName } = $content.childNodes[i]
				if (nodeName.toLowerCase() == 'img') emojiTimes++
			}
			this.total = $content.innerText.replace(/\s{1}[\r\n]/g, '-').trim().length + emojiTimes
			if (this.max !== 0 && this.total > this.max){
				let out = '', i = 0
				for (let c = 0; c < $content.childNodes.length; c++) {
					if (i > this.max) break
					const $c = $content.childNodes[c]
					if ($c.nodeName.toLowerCase() == 'img') {
						out += $c.outerHTML
						i++
					} else {
						const $n = $c.nodeValue, len = $n.length
						i += len
						i <= this.max ? out += $n : out += $n.substr(0, len + this.max - i)
					}
				}
				this.content = out
				$content.innerHTML = out
				this.total = this.max
				let range = this.range,
					selection = getSelection()
				if (!range) range = document.createRange()
				range.selectNodeContents($content)
				range.collapse(false)
				selection.removeAllRanges()
				selection.addRange(range)
				return false
			}
			return true
		},
		input(){
			//定时器确保compositionend已经执行
			setTimeout(() => {
				if (!this.canEdit || this.typing || !this.calc() || (this.max !== 0 && this.total >= this.max)) return
				const $content = document.querySelector('#contenteditable'),
					child = $content.childNodes
				$content.scrollTop = $content.offsetHeight
				this.content = [...child].map(i => i.nodeName.toLowerCase() == 'img' ? i.outerHTML : i.nodeValue).join('')
			}, 0)
		},
		enter(e){
			//点击或聚焦
			if (e.target.id != 'contenteditable') return
			const selection = getSelection()
			if (!selection) return
			const node = selection.anchorNode
			if (!node) return
			this.range = selection.getRangeAt(0)
			this.startOffset = this.range.startOffset
		},
		addEmoji(src){
			//添加Emoji
			if (this.disabled) return
			if (this.max !== 0 && this.total >= this.max) return
			let $content = document.querySelector('#contenteditable'),
				range = this.range,
				selection = getSelection(),
				emoji = document.createElement("img")
			emoji.src = src;
			emoji.setAttribute('style', this.imgStyle)
			if (!range || !selection.anchorNode) {
				range = document.createRange()
				range.selectNodeContents($content)
				$content.focus()
			}
			selection.deleteFromDocument()
			const	textNode = range.startContainer,
				child = $content.childNodes
			if (selection.anchorNode.nodeName != '#text') {
				if (child.length > 0) {
					for (let i = 0; i <= child.length; i++) {
						if (i == selection.anchorOffset) {
							$content.insertBefore(emoji, child[i])
							child[i + 1] ? range.setStartBefore(child[i + 1]) : range.selectNodeContents($content)
							break
						}
					}
				} else {
					$content.appendChild(emoji)
					range.selectNodeContents($content)
				}
			} else {
				range.insertNode(emoji)
				range.setStart(textNode, this.startOffset > textNode.length ? 0 : this.startOffset)
			}
			this.calc()
			this.content = [...child].map(i => i.nodeName.toLowerCase() == 'img' ? i.outerHTML : i.nodeValue).join('')
			range.collapse(false)
			selection.removeAllRanges()
			selection.addRange(range)
		}
	}
}
</script>

<style lang="scss" scoped>
	.emoji {
		.teatarea {
			width: 100%;
			margin: 0 auto;
			.field {
				position: relative;
				width: 100%;
				#contenteditable {
				
					padding: 2px 2px 2px;
					line-height: 1.8;
					max-height: 100px;
					font-size: 16px;
					text-align: left;
					box-sizing: border-box;
					outline: none;
					overflow-y: auto;
					cursor: text;
					transition: all ease .4s;
					border: 1px solid #ddd;
					border-radius: 5px;
					overflow-x: hidden;
					&:focus {
						border: 1px solid #409eff;
					}
					&[contenteditable = "false"] {
						cursor: not-allowed;
						&.forbid {
							cursor: text;
						}
					}
					&:empty::before {
						color: #ddd;
						content: attr(placeholder);
					}
					&.wordLimit {
						padding-bottom:5px;
						padding-top: 5px;
					}
				}
				.total, .clear {
					position: absolute;
					bottom: 1px;
					left: 12px;
					background: #fff;
					color: #aaa;
					font-size: 16px;
					padding: 6px;
					pointer-events: none;
				}
				.clear {
					left: auto;
					right: 12px;
					bottom: 4px;
					cursor: pointer;
					padding: 0;
					pointer-events: all;
				}
			}
			.button {
				background: #409eff;
				margin: 0 8px;
				padding: 6px 10px;
				color: #fff;
				border-radius: 5px;
				cursor: pointer;
				border: 0;
				font-size: 16px;
				outline: none;
				&:active {
					border: 0;
					outline: none;
				}
				&:hover {
					opacity: .8;
				}
			}
		}
	}
</style>
