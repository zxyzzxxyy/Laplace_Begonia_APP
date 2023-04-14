<template>
	<view style="height:100vh;display: flex;flex-direction: column;justify-content: center;align-items: center;">
		<image src="../../static/book.png" style="height:65px;width:65px;margin-top: 10px;margin-bottom: 10px;"></image>
		<p style="font-size: 25px;">学伴 WMU v{{version.appWgtVersion}}</p>
		<p style="font-size: 20px;">SpringBoot v2.0</p>
		<p style="font-size: 20px;">uni-app v3.7.3</p>
		<view style="display: flex;flex-direction: column;justify-content: center;align-items: center;margin-top: 10px;">
			<p style="font-size: 25px;">主创团队</p>
			<p style="font-size: 22px;margin-top: 5px">指导教师</p>
			<p>邵英安</p>
			<p style="font-size: 22px;margin-top: 10px">软件开发</p>
			<p>计算机科学学院</p>
			<p>2019级软件工程 赵欣宇</p>
			<p style="font-size: 22px;margin-top: 10px">美术设计</p>
			<p>美术学院</p>
			<p>2019级视觉传达设计 韩丹丹</p>
			<p style="font-size: 22px;margin-top: 10px">项目策划</p>
			<p>计算机科学学院</p>
			<p>2019级软件工程 沈银兰</p>
			<p>2020级软件工程 徐梓倩</p>
			<p style="font-size: 22px;margin-top: 10px">媒体推广</p>
			<p>计算机科学学院</p>
			<p>2020级软件工程 陈翰新</p>
		</view>
		
		<p style="font-size: 18px;margin-top: 20px;">2022-3-24 v1.0.00 —— 2023-3-7 v2.0.00</p>
		<p style="color: #3DA7FF;font-size: 20px;margin-top: 10px;" @click="test1()">
			<text>抖音 三味邮驿</text>
		</p>
		<view style="width:80vw">
		<p style="font-size: 17px;margin-top: 10px;text-align: center;">此项目依然存在一些问题以及未能实现的细节，若发现错误或者设计不合理的地方，欢迎提出一起探讨解决。</p>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				version:{},
				x:"",
				y:"",
				z:"",
				direction:"",
				color:"white",
				color1:"black",
			}
		},
		methods: {
			test(){
				uni.navigateTo({
					url:"/pages/index/outpage?url=https://blog.txtz.link"
				})
			},
		test1:function(){
				uni.navigateTo({
					url:"/pages/index/outpage?url=https://v.douyin.com/R2jkTyb/"
				})
			},
			back(){
				uni.navigateBack();
			},
		},
		onLoad(){
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
		},
		onShow() {
			let that=this;
			
			uni.getSystemInfo({
				success: function (res) {
					that.version=res
				}
			});
			plus.runtime.getProperty(plus.runtime.appid, (wgtinfo) => {
			        this.version.version = wgtinfo.version;
			        //this.versionCode = wgtinfo.versionCode ;
			    // console.log(innerVer)
			})
			const callback = function (res) {
			
			}
			uni.onMemoryWarning(callback);
			uni.onAccelerometerChange(function (res) {
				that.x=res.x;
				that.y=res.y;
				that.z=res.z;
			});
			const callbac = function (res) {
				that.direction=(res.direction);
			}
			uni.onCompassChange(callbac);
		
		}
	}
</script>

<style>

</style>
