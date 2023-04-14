<template>
	<view>
		<view style="width:100vw;height:45px;display: flex;flex-direction: row;align-items: center;justify-content: center;padding-top:4.2vh;border-bottom: 1px solid #e6ebf4;margin-bottom: 0px;
		position:fixed;top:0;background-color:white;z-index:2
		"
		:style="{backgroundColor:color}"
		>
			<view style="width:33vw;display: flex;align-items: center;">
				<u-icon name="arrow-left" size="20" style="margin-left: 2vw;" :color="color1" @click="back()"></u-icon>
			</view>
			<view style="width:33vw;display: flex;flex-direction: row;align-items: center;justify-content: center">
				<text style="font-weight: 700;" :style="{color:color1}">浏览历史</text>
			</view>
			<view style="width:33vw">
				<view 
				:style="{color:color1}"
				style="margin-left: auto;width:32px;margin-right: 2vw;" @click="delete1()">清空</view>
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;">
			1
		</view>
		<view v-for="(item,index) in themelist"
		@click="totheme(item.themeid)"
		>
		<view  style="display: flex;flex-direction: column;min-height:60px;justify-content: center;">
			<view style="width:96vw;margin-left: 2vw;height:16px" v-if="item.title.length>0">
				{{item.title}}
			</view>
			<view style="width:100%;height:20px;opacity:0" v-if="item.title.length>0&&item.data.length>0">
				1
			</view>
			<view style="width:96vw;margin-left: 2vw;height:15px" v-if="item.data.length>0">
				<u--text :text="item.data" lines="1" color="#93909e" size="15"></u--text>
			</view>	
		</view>
		<u-divider style="margin-bottom: 15px;"></u-divider>
		</view>
		<view style="margin-top: 10px;width:100vw;display: flex;flex-direction: column;align-items: center;justify-content: center">
			<text style="font-size: 14px;color:#93909e">没有更多了</text>
			
		</view>
		<view style="width:100vw;height:10px;opacity:0">1</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				themelist:[],
				color:"white",
				color1:"black",
			}
		},
		methods: {
			back(){
				uni.navigateBack()
			},
			totheme(i){
				uni.navigateTo({
					url:"/pages/index/theme?themeid="+i
				})
			},
			delete1(){
				getApp().globalData.history=[];
				this.themelist=getApp().globalData.history;
			}
		},
		onLoad(){
			if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
			}
			this.themelist=getApp().globalData.history;
			this.themelist.sort(function(a,b){
				return a.time<b.time?1:-1;
			});
			if(getApp().globalData.skinchoose!=0&&getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor=='white')
			uni.setNavigationBarColor({
				frontColor:"#ffffff",
				backgroundColor:''
			})
			else
			uni.setNavigationBarColor({
				frontColor:"#000000",
				backgroundColor:''
			})
		}
	}
</script>

<style>

</style>
