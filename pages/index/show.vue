<template>
	<view style="background: linear-gradient(to bottom right, rgb(124, 163, 255) , rgb(16, 216, 255));;height:100vh;width:100vw;display: flex;justify-content: center;
	background-attachment: fixed;background-position:center;
	display: flex;flex-direction: column;align-items: center;justify-content: center;	
	overflow: hidden;
	" :class="{'a1':op==2,'a2':op==1,'a3':op==0}"
	>
	<image :src="showback.url" style="width:100vh;height:100%;position: absolute;overflow-y: hidden;z-index: 7;"
	 mode="aspectFit" v-if="toshouye==1||toshouye==2"
	>
		<view style="width:100%;height:100%;background-color: rgba(0,0,0,0.35);z-index: 7;">
		<u--image :fade="false" src="../../static/1.jpg"  width="75vw" style="margin-top: 25vh;"
		v-if="showback==null" mode="aspectFill"
		></u--image>
		<view style="z-index: 8;position: absolute;font-size: 14px;color:white;margin-left: 90%;margin-top: 10%;">
			<text @click="delete1()">跳过</text>
		</view>
		<view style="z-index: 8;width:100%;height:100%;display: flex;align-items: center;justify-content: center;">
			<text style="font-size: 50px;color:white;text-shadow: 3px 3px black;margin-top: -20vh;">学伴 WMU</text>
		</view>
		<view style="z-index: 8;bottom:10px;position: absolute;font-size: 12px;color:white;margin-left: 3%;">
			 <view  v-if="showback.pid!=null">{{showback.title}} <br> pid:{{showback.pid}} <br> 画师：{{showback.username}}</view>
		</view>
		</view>
		</image>
	</view>
</template>

<script>
	import { pathToBase64, base64ToPath } from '../../js_sdk/mmmm-image-tools/index.js'
	export default {
		data() {
			return {
				showback:{},
				e:"",
				h:0,
				toshouye:0,
				op:2
			}
		},
		beforeCreate() {
			{
				let _this =this;
				setTimeout(function() {
				    {
						 plus.navigator.closeSplashscreen();
						if(_this.op==2)
						_this.stop2(1);	
					
					}	
				 }, 4000);
				uni.getSystemInfo({
							success: res => {
								_this.h = res.windowHeight;
								
							}
						});
				uni.request({
					url:getApp().globalData.http+"/api/getpixiv",
					method:"POST",
					data:{
						"type":2
					},
					success: (res) => {
							this.showback=res.data[0];
							var url = res.data[0].url;
							var name = url.split("/",4)[3];
							var sub=-1;	
							uni.getStorage({
							    key:"pixiv",
							    success: function(res){
							        getApp().globalData.pixiv=res.data;
									//console.log("admin:"+getApp().globalData.admin);
								}
							 });
						
							for(var i=0;i<getApp().globalData.pixiv.length;i++){
								
								if(getApp().globalData.pixiv[i].name==name){
									sub=i;
									_this.toshouye=1;
									var temp1="";
									/*pathToBase64(getApp().globalData.pixiv[i].url)
									  .then(base64 => {
										console.log(base64);
										temp1=base64;
									})*/
									this.showback.url=getApp().globalData.pixiv[i].url;
								
							
									_this.e=null;
					
									 return;
								}
							}
							if(sub==-1){
								uni.downloadFile({
									url: url, 
										success: (res) => {
										
											if (res.statusCode === 200) {
												_this.toshouye=1;
												_this.e=null;
												_this.showback.url=res.tempFilePath;
														if(_this.op==2)
														_this.stop2(2);	
												uni.saveFile({
												    tempFilePath: res.tempFilePath,
												    success: function (res1) {
												
														var temp=getApp().globalData.pixiv;
														temp.push({"name":name,"url":res1.savedFilePath});
														uni.setStorage({
														    key: "pixiv",
														    data: temp,
														    success: function () {
														    }
														});
													
												    }
												});
											
											}
										}
								})
							}
					}
				})
				 
			}	
		},
		methods: {
			abc(){
		
			},
			stop2(e){	
				uni.$u.throttle(this.stop1(e), 10000);
			},
			stop1(e) {
				if(this.op==0)return;
				{
					let _this=this;
					setTimeout(function() {
					_this.op=1;
					
					setTimeout(function() {
					  _this.op=0;
						getApp().globalData.showpage=0;
						_this.$emit("changeshowpage","1");
					 }, 300);
					
				},6000)
				}
			},
			stop(){
				var box=function(e){passive: false ;};
					document.body.style.overflow='hidden';
					document.addEventListener("touchmove",box,false);
			},
			delete1(){
				this.op=1;
				let _this=this;
				setTimeout(function() {
					getApp().globalData.showpage=0;
					_this.op=0;
					_this.$emit("changeshowpage","2");
					}
				, 300);
			}
		}
	}
</script>

<style>
	.a2{
		z-index: 8;
		opacity: 0;
		transition: 0.3s;
	}
	.a1{
		z-index: 8;
		opacity: 1;
		transition: 0.3s;
	}
	.a3{
		z-index: -1;
		opacity: 0;
		display: none;
	}
	.re1{
		animation: myfirst 10s  linear
	}
	@keyframes myfirst
	{
		0%{
			transform: scale(1);
		}

		100%{
			transform: scale(1.15);
		}
	}
</style>
