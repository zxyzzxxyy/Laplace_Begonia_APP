<template>
	<view>
		<view style="width:100vw;height:45px;display: flex;flex-direction: row;align-items: center;justify-content: center;padding-top:4.2vh;border-bottom: 1px solid #e6ebf4;margin-bottom: 15px;
		position:fixed;top:0;z-index:2
		"
		:style="{backgroundColor:color}"
		>
			<view style="width:33vw;display: flex;align-items: center;">
				<u-icon
				 :color="color1"
				 name="arrow-left" size="20" style="margin-left: 2vw;" @click="back()"></u-icon>
			</view>
			<view style="width:33vw;display: flex;flex-direction: row;align-items: center;justify-content: center">
				<text
				 :style="{color:color1}"
				 style="font-weight: 700;">设置</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:15px">
			1
		</view>
		<view style='width:100vw'>
			<view style="margin-top: 10px;margin-left: 2.5vw;font-size: 14px;" @click="settoutu()">
				<text>修改背景图</text>
			</view>
			<u-divider ></u-divider>
			<view style="margin-top: 10px;margin-left: 2.5vw;font-size: 14px;" @click="changemain()">
				<text>切换主题装扮</text>
			</view>
			<u-divider ></u-divider>
			<view style="margin-top: 10px;margin-left: 2.5vw;font-size: 14px;" @click="setpassword()">
				<text>修改密码</text>
			</view>
			<u-divider ></u-divider>
			<view style="margin-top: 10px;margin-left: 2.5vw;font-size: 14px;" @click="about()">
				<text>关于</text>
			</view>
			<u-divider ></u-divider>
		</view>
		<view style='width:100vw'>
			<u-button  text="退出登录" type="error" @click="show=true"></u-button>
		</view>
			<view >
				<u-modal :show="show" title="退出登录" content='是否退出登录' :closeOnClickOverlay="true" @cancel="show=false" :showCancelButton="true" @close="show=false" @confirm="loginout()"></u-modal>
			</view>
			<uni-popup ref="popup" type="dialog">
			    <uni-popup-dialog mode="input" placeholder="请输入签名内容" type="success" :duration="2000" :before-close="true" @close="close" @confirm="confirm"></uni-popup-dialog>
			</uni-popup>
			<u-toast ref="uToast"></u-toast>
			<gpp-date-picker @onCancel="closetime" @onConfirm="setbirthday" ref="time" :endDate="endDate">
			    {{pickerDate}}
			</gpp-date-picker>
	</view>
</template>

<script>
	import gppDatePicker from "@/components/gpp-datePicker/gpp-datePicker.vue"
	export default {
		components:{
		    gppDatePicker
		},
		data() {
			return {
				color:"white",
				color1:"black",
				show:false,
				show1:false,
				show2:false,
				birthday:"",
				endDate:"",
				pickerDate:"",
				mainname:"默认主题",
				upload:[
					{
						type: 'success',
						icon: false,
						title: '成功主题',
						message: "设置成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "设置失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "其它设备登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "请登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					}
				]
			}
		},
		onLoad() {
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
			if(getApp().globalData.skinchoose==1){
				this.mainname="默认主题";
			}else this.mainname="東雪莲"
			 var nowDate = new Date();
			      var date = {
			        year: nowDate.getFullYear(),
			        month: nowDate.getMonth() + 1,
			        day: nowDate.getDate(),
			      }
			      var dayDate = date.year + '-' + (date.month >= 10 ? date.month : '0' + date.month) + '-' + (date.day >= 10 ? date.day : '0' + date.day);
				  this.endDate=dayDate;
		},
		methods: {
			back(){
				uni.navigateBack();
			},
			setheadborder(){
				uni.navigateTo({
					url:"/pages/index/myheadborder/myheadborder"
				})
			},
			about(){
				uni.navigateTo({
					url:"/pages/index/about"
				})
			},
			opentime(){
				this.$refs.time.show();
			},
			closetime(){
				this.$refs.time.hide();
			},
			changemain(){
				uni.navigateTo({
					url:"skin/skin"
				})
			},
			changemain1(){
				if(getApp().globalData.skinchoose==0){
					getApp().globalData.skinchoose=1;
				}else{
					getApp().globalData.skinchoose=0;
				}
				uni.setStorage({
				    key: "skinchoose",
				    data: getApp().globalData.skinchoose,
				    success: function () {
				    }
				});
				this.show2=false;
				plus.runtime.restart();

			},
			setbirthday(e){
			//	console.log(e.dateValue);
				var date = new Date(e.dateValue);
				var time1= date.getTime()/1000;
				uni.request({
					url:getApp().globalData.http+"/api/setbirthday",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"birthday":time1
					},
					success: (res) => {
						if(res.data.code==1001){
				
							this.$refs.uToast.show({
								...this.upload[0],
								complete() {
									return;
								}
							})
						}
					},
					fail: () => {
						{
				
							this.$refs.uToast.show({
								...this.upload[1],
								complete() {
									return;
								}
							})
						}
					}
				})
			},
			open() {
				this.$refs.popup.open()
			},
					close() {
						// TODO 做一些其他的事情，before-close 为true的情况下，手动执行 close 才会关闭对话框
						// ...
						this.$refs.popup.close()
					},
					

			confirm:function(value) {
				this.$refs.popup.close();
				uni.request({
					url:getApp().globalData.http+"/api/setsign",
					method:'POST',
					data:{
						"sign":value,
						"cookie":getApp().globalData.cookie
					},
					success:(res) =>{
						if(res.data.code==1001){
							this.sign=value;
							this.$refs.uToast.show({
								...this.upload[0],
								complete() {
									return;
								}
							})
						}
					},
					fail: (res) => {
						this.$refs.uToast.show({
							...this.upload[1],
							complete() {
								return;
							}
						})
					}
				});
			},
				
			setpassword:function(){
				uni.navigateTo({
					url:"changepassword"
				})
			},
			settoutu:function(){
				uni.chooseImage({
					count: 1,
					sizeType: ['original', 'compressed'],
					sourceType: ['album'],
					success: function(res) {
						//console.log(res.tempFilePaths);
						uni.uploadFile({
						    url:"https://www.txtz.club:8808/api/upload",		//post请求的地址
						    filePath:res.tempFilePaths[0],
						    name:'file',	
						    success: (res) => {
									 res.data = JSON.parse(res.data)
									
								uni.request({
									url:getApp().globalData.http+"/api/setusertoutu",
									method:"POST",
									data:{
										"toutu":res.data.location,
										"userid":getApp().globalData.userid,
										"cookie":getApp().globalData.cookie
									},
									success: (res1) => {
										if(res1.data.code==1001){
											this.toutu=res.data.location;		
											uni.navigateBack({
												delta:1
											})
										}
										else{
											this.$refs.uToast.show({
												...this.upload[1],
												complete() {
													return;
												}
											})
										}
									},
									fail:(res)=>{
										this.$refs.uToast.show({
											...this.upload[1],
											complete() {
												return;
											}
										})
									}
								})
							}
						})
					}
				});
			},
			loginout(){
				getApp().globalData.username='';
				getApp().globalData.userheadimage='';
				getApp().globalData.userbackgroundimage='';
				getApp().globalData.cookie='';
				getApp().globalData.sign='';
				getApp().globalData.save='';
				getApp().globalData.bylike='';
				getApp().globalData.registertime='';
				getApp().globalData.userid='';
				getApp().globalData.admin='';
				getApp().globalData.mylike=[];
				getApp().globalData.replymessage=[];
				getApp().globalData.chat=[];
				getApp().globalData.chatlist=[];
				uni.setStorage({
				    key: "mylike",
				    data: getApp().globalData.mylike,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "chatlist",
				    data: getApp().globalData.chatlist,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "chat",
				    data: getApp().globalData.chat,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "replymessage",
				    data: getApp().globalData.replymessage,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "admin",
				    data: getApp().globalData.admin,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "userid",
				    data: getApp().globalData.userid,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "username",
				    data: getApp().globalData.username,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "username",
				    data: getApp().globalData.username,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "userheadimage",
				    data: getApp().globalData.userheadimage,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "userbackgroundimage",
				    data: getApp().globalData.userbackgroundimage,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "cookie",
				    data: getApp().globalData.cookie,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "save",
				    data: getApp().globalData.save,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "bylike",
				    data: getApp().globalData.bylike,
				    success: function () {
				    }
				});
				uni.setStorage({
				    key: "registertime",
				    data: getApp().globalData.registertime,
				    success: function () {
				    }
				});
				uni.reLaunch({
					url:"/pages/index/index"
				})
			}
		}
	}
</script>

<style>

</style>
