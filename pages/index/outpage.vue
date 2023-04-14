<template>
	<view>
		<view style="width:100vw;height:45px;display: flex;flex-direction: row;align-items: center;justify-content: center;padding-top:4.2vh;border-bottom: 1px solid #e6ebf4;margin-bottom: 15px;
		position:fixed;top:0;background-color:white;z-index:2
		"
		:style="{backgroundColor:color}"
		>
			<view style="width:33vw;display: flex;align-items: center;">
				<u-icon name="arrow-left" size="20" style="margin-left: 2vw;" @click="back()"></u-icon>
			</view>
			<view style="width:33vw;display: flex;flex-direction: row;align-items: center;justify-content: center">
				<text style="font-weight: 700;"></text>
			</view>
			<view style="width:33vw">
				<view 
				:style="{color:color1}"
				style="margin-left: auto;width:32px;margin-right: 2vw;" ></view>
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:15px">
			1
		</view>
		<web-view :src="url" style="width: 100%;height:100%;">
			
		</web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				url:"",
				color:"white",
				color1:"black",
			}
		},
		methods: {
			back(){
				uni.navigateBack();
			}
		},
		onLoad:function(option){
			if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
			}
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
			this.url=option.url;
		//	console.log(this.url);
		},
	}
</script>

<style>

</style>
