<template>
	<view style="background-color: white;height:100vh;width:100vw;overflow-x: hidden;">
		<!--顶部栏-->
		<view style="margin-top: 5vh;;height:5vh;display: flex;justify-content: center;align-items: center;position: relative;width: 100vw;">
			<text>发布帖子</text>
			<view style="position: absolute;left:0;margin-left: 4vw;">
				<u-icon name="close" size="18" color="black" @click="back()"></u-icon>
			</view>
			<view style="position: absolute;right:0;margin-left: auto;margin-right: 4vw;color:#aa55ff "
			@click="fabu()"
			>
				发布
			</view>
		</view>
		<view style="margin-top: 20px;margin-left:2vw;width:96vw">
				<u--textarea
				   placeholder="标题"
				   border="none"
				   size="19"
				   :adjust-position="false"
				   v-model="title"
				   maxlength="20"
					style="width:100%;"
				height="20"
				 ></u--textarea>
				<u-divider></u-divider>
			<view style="width:100%;position:relative;;">
				<textarea 
				border="none" 
				maxlength="2000"  
				style="width:96%;padding:10px;font-size: 15px;color:#303133"
				:adjust-position="false" 
				v-model="text" 
				placeholder-style="color:#c0c4cc;font-size:15px"
				placeholder="请输入内容" 
				autoHeight 
				count
				>
				</textarea>
				<view style="position: absolute;bottom:0;right:0;font-size: 12px;color:#c0c4cc;margin-bottom:-10px;">
					{{text.length+'/1000'}}
				</view>
			</view>
			<u-divider></u-divider>
			<view  style="display: flex;flex-direction: row;flex-wrap: wrap;">
				<image v-for="(item,index) in uploadimages" :src="item"
				@click="deleteimage(index)" mode="aspectFill" 
				style="height:30vw;width:30vw;margin-right:1vw;margin-left: 1vw;;border-radius: 15px;margin-top:2vw"></u--image>
				<view 
				@click="add_image()"
				style="
					background-color: #f6faff;border:1px dashed #ecf0f4;
					height:30vw;width:30vw;margin-right:0vw;margin-left: 1vw;
					border-radius: 15px;margin-top:2vw;
					display: flex;flex-direction: column;align-items: center;justify-content:center">
					<u-icon name="plus" color="#909399" size="28"></u-icon>
					<text style="color:#909399;font-size:14px">上传图片</text>
				</view>
			</view>
		</view>
		<view style="display: flex;flex-direction: column;align-items: center;width:100vw;background-size: cover;background-attachment: fixed;overflow-y: hidden;overflow-x: hidden" >
			
			<view style=";background-color: white;width:95vw;;background-color: white;padding-left:2.5vw;padding-right:2.5vw;"  :style="{'opacity':op}">


			<view style="display: flex;flex-direction: row;flex-wrap:wrap;width:100vw;margin-top:10px" >
				<u-tag v-for="(item,index) in tags" :text="item"  icon="tags-fill" style="width: auto;margin:10px" @click="delete_tag(item)" plain plainFill></u-tag>
				<view style="display: flex;flex-direction: row;align-items: center;" v-if="tags.length<5">
				<u--input
				   placeholder="添加标签"
				   border="bottom"
				   maxlength="10"
				   v-model="tag"
					style="width:20vw;margin-bottom: 10px;"
					
				 />
				 <u-button type="primary" :plain="true" text="添加" @click="add_tag()" style="width:50px;margin-right: auto;margin:0;margin-left: 5px;height:30px;"></u-button>
				 
				</view>
			</view>
			<view>
				<u--text prefixIcon="map-fill" iconStyle="color:#3c9cff;margin-right:5px" v-if="position==''" type="primary" :plain="true" text="添加地点" color="#3c9cff" @click="setposition" style="width:auto;margin:0;height:30px;"></u--text>
				<u--text prefixIcon="map-fill" iconStyle="color:#3c9cff;margin-right:5px" v-if="position!=''" type="primary" :plain="true" :text="position" @click="setposition" style="width:auto;margin:0;height:30px;"></u--text>
			</view>
			<view style="display: flex;flex-direction: row;align-items: center;height:50px">
				<view style="">
				<u-tag v-if="type==2" type="primary" :plain="true" text="原创" @click="yuanchuang=true;type=0" style="width:50px;margin:0;height:30px;"></u-tag>
					
				<u-tag  plain plainFill  v-if="type==0" text="原创" @click="yuanchuang=false;type=1" style="width:50px;margin:0;height:30px;" ></u-tag>
				</view>
				<u--input
				   placeholder="原文链接(必填)"
				   border="bottom"
				   size="19"
				   v-model="ycsrc"
					style=";margin-bottom: 10px;"
					v-if="type==1"
				 />
				 <u-tag type="primary" :plain="true" text="搬运" @click="yuanchuang=true;type=2" style="width:50px;margin-right: auto;margin:0;margin-left: 5px;height:30px;" v-if="yuanchuang==false"></u-tag>
			</view>
			<view style="display: flex;flex-direction: row;align-items: center;flex-wrap: wrap;">
					<view v-for="(item,index) in fenlei">
					<u-tag  :text="item"  icon="tags-fill" style="width: auto;margin-right:10px;
					margin-top:10px;margin-bottom:10px"
					 plain plainFill v-if="index==fenleisub"></u-tag>
					<u-tag  :text="item"  icon="tags-fill" style="width: auto;margin-right:10px;
					margin-top:10px;margin-bottom:10px" plain v-if="index!=fenleisub"  @click="fenleisub=index,fenlei1=item"></u-tag>
					</view>
				</view>
			</view>
		</view>
		<view v-if="keyborde!=0" style="width:100vw;opacity: 0;"  :style="{height:keyborde+'px'}" >
			123
		</view>
	</view>
</template>

<script>
	import jinEdit from '../../components/jin-edit/jin-edit.vue';
	export default {
		components: {
		jinEdit
		},
		data() {
			
			return {
				keyborde:0,
				op:0.95,
				yuanchuang:true,
				fenleisub:0,
				ycsrc:"",
				icon:"/static/icon.png",
				userbackgroundimage:"",
				userheadimage:"",
				src:"/static/aa.jpg",
				data:"",
				username:"",
				text:"",
				image:[],
				admin:0,
				title:"",
				tags:[],
				key:"",
				tag:"",
				fenlei:[],
				uploadimages:[],
				fenlei1:"默认分类",
				type:2,
				hw:[],
				position:"",
				lal:"",
				upload:[
					{
						type: 'error',
						title: "失败",
						message:"其它设备登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					}
				]
			}
		},
		onLoad() {
			let that=this;
			uni.onKeyboardHeightChange(res => {
			  that.keyborde=res.height
			  if(res.height>0){
				  that.textarea1=60;
			  }else that.textarea1=20;
			})
		},
		onShow() {
		
			let that = this;
			if(getApp().globalData.cookie=='')
			{
				uni.reLaunch({
					url:"index"
				})
				return;
			}
			else
			uni.request({
				url:getApp().globalData.http+"/api/jugeuser",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie
				},
				success: (res) => {
					if(res.data.code==1002){
						this.$refs.uToast.show({
							...this.upload[0],
							complete() {
								that.loginout();
							}
						})

					}
				}
			})
			this.userbackgroundimage=getApp().globalData.userbackgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			this.admin=getApp().globalData.admin;
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					////console.log("admin:"+getApp().globalData.admin);
					this.op=res.data;
				}
			 });
			this.op=getApp().globalData.op;
			this.fenlei=[];
			uni.request({
				url:getApp().globalData.http+"/api/getfenleilist",
				method:"POST",
				data:{
				},
				success: (res) => {
					for(var i=0;i<res.data.length;i++)
					this.fenlei.push(res.data[i]);
				}
			})
		},
		methods: {
			deleteimage:function(e){
				this.uploadimages.splice(e,1);
				this.hw.splice(e,1);
			},
			change_fenleisub:function(e){
			
				this.fenleisub=e;
			},

			delete_tag:function(e){
				this.tags.splice(this.tags.indexOf(e),1);
			},
			add_tag:function(){
				if(this.tag.length>0)
				this.tags.push(this.tag);
				this.tag=""
			},
			GetChange:function(e){
			//	console.log(e);
			},
			add_image(){
				let _this=this;
				uni.chooseImage({
					count: 1,
					sizeType: [ 'compressed'],
					sourceType: ['album'],
					success: function(res) {
						//console.log(res.tempFilePaths);
						uni.getImageInfo({
							src:res.tempFilePaths[0],
							success:(res)=>{
								var temp={
									width:res.width,
									height:res.height
								}
								_this.hw.push(temp);
							}
						})
						uni.uploadFile({
						    url:"https://www.txtz.club:8808/api/upload",		//post请求的地址
						    filePath:res.tempFilePaths[0],
						    name:'file',	
						    success: (res) => {

								res.data = JSON.parse(res.data)
								var location = res.data.location;
								_this.uploadimages.push(location);
								
							}
						})
					}
				});
				
			},
			con:function(e){
				this.text=e;
				////console.log(this.text);
			},
			setposition(){
				let that=this;
				uni.chooseLocation({
					success: function (res) {
						that.position=res.name;
						that.lal=res.latitude+";"+res.longitude
					}
				});
			},
			back:function(){
				uni.reLaunch({
					url:"index"
				})
			},
			fabu:function(){
				//console.log(res);
				if(this.fenlei1=="绘画"&&this.uploadimages.length<1){
					uni.showToast({
						title:"绘画区至少上传一张图片",
						icon:"error"
					})
					return;
				}
				if(this.type==1&&this.ycsrc==''){
					uni.showToast({
						title:"原文链接不能为空",
						icon:"error"
					})
					return;
				}
				var re1 = new RegExp("<.+?>","g");//匹配html标签的正则表达式，"g"是搜索匹配多个符合的内容
				var msg = this.text.replace(re1,'');//执行替换成空字符
				
				msg=msg.toString();
				////console.log(this.text);
			//	console.log(msg);
				////console.log(temp);
			
				
				var g = new Date().getTime();
				
				msg=msg.replace(/[\r\n]/g,"");
				if(msg.length==0){
					uni.showToast({
						title:"内容不能为空",
						icon:"error"
					})
					return;
				}
				var g = new Date().getTime();
				var tag="";
				for(var i=0;i<this.tags.length;i++){
					if(this.tags[i].length==0)
						continue;
					tag+=this.tags[i]+";";
				}
				var images1="";
				var text1=this.text;
				for(var i=0;i<this.uploadimages.length;i++){
					
					images1=images1+this.uploadimages[i]+";";
					text1+="<img src="+"'"+this.uploadimages[i]+"'"+" mode='aspectFit' style='border-radius:5px;margin-top:5px;width:100%;height:auto'/>"
				}
				text1 = text1.replace(/\n/g, '<br/>');
				msg = msg.replace(/&nbsp;/ig, '');
				msg = msg.replace(/&rdquo;/ig, '');
				msg = msg.replace(/&middot;/ig, '');
				msg = msg.replace(/&mdash;/ig, '');
				msg = msg.replace(/&ldquo;/ig, '');
				msg = msg.replace(/\s/ig, '');
				uni.request({
					url:getApp().globalData.http+"/api/newtheme",
					method:"POST",
					data:{
						"title":this.title,
						"text":text1,
						"image":images1,
						"data":msg,
						"userid":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"createtime":parseInt(g/1000),
						"tags":tag,
						"type":this.type,
						"ycsrc":this.ycsrc,
						"fenlei":this.fenlei1,
						"lal":this.lal,
						"position":this.position
					},
					success: (res) => {
						//console.log(res);
						if(res.data.code==1001)
						uni.showToast({
							title:"发布成功",
							icon:"success"
						})
						else if(res.data.code==1002){
							uni.showToast({
								title:"账号禁用中",
								icon:"error"
							})
						}
						setTimeout(() => {  
							uni.navigateBack({
								
							})}
							, 1000)
					},
					fail: (res) => {
						console.log(res);
						uni.showToast({
							title:"发布失败",
							icon:"error"
						})
					}
				})
			},

		
		}
	}
</script>

<style>
.op{
	opacity: 0.95; 
}
</style>
