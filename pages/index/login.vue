<template>
	<view style="background-color: white;;min-width:1920px;width:100vw;height:100vh;background-size: cover;background-attachment: fixed;overflow-y: hidden;"  id="body">
		<!--顶部栏-->
	
		
		<view style="width: 100vw;height:85vh;margin-top: 0vh;background-color: white;display: flex;align-items: center;flex-direction: column;padding-top: 5vh;">
			<view style="width:95vw;margin-bottom: 10vh;padding-left: 5vw;">
				<u-icon name="arrow-left" size="25" @click="back()"></u-icon>
			</view>
			<view style="margin-top: 3%;">
				<text style="font-size: 24px;font-weight: 700;">登录</text>
			</view>
			<view style="width:80%;margin:20px">
				<view>
					<text style="font-size: 18px;font-weight: 500;">邮箱</text>
				</view>
				  <u--input
				    placeholder="请输入邮箱"
				    clearable
					style="margin-top:20px;margin-bottom: 20px;"
					v-model="email"
					:adjust-position="false"
				  ></u--input>
				<view>
					<text style="font-size: 18px;font-weight: 500;">密码</text>
				</view>
				  <u--input
				    placeholder="请输入密码"
				    clearable
					style=";margin-top:20px;margin-bottom: 40px;"
					v-model="password"
					password
					@confirm="login()"
					:adjust-position="false"
				  ></u--input>
				<view style="width: 100%;"  @click="login()">
				  <u-button text="登录" type="primary"></u-button>
				</view>
				<view style="margin-top: 20px;display: flex;align-items: center;justify-content: center;flex-direction: row;">
					<text style="font-size: 16px;margin-right:4px">没有账号?</text><text style="font-size: 16px;color:#3c9cff" @click="register()">去注册</text>
				</view>
				<view style="margin-top: 20px;display: flex;align-items: center;justify-content: center;flex-direction: row;">
					<text style="font-size: 16px;color:#3c9cff" @click="findpassword()">找回密码</text>
				</view>
			</view>
		</view>
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	import md5 from '@/pages/md5.js'
	export default {

		data() {
			return {
				email:"",
				password:"",
				username:"",
				key:"",
				op:1,
				backgroundimage:"",
				icon:"../../static/icon.png",
				list:[
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "邮箱格式错误",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "密码长度小于7位",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "邮箱或密码错误",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "邮箱未激活",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "登陆失败",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
											type: 'success',
											icon: false,
											title: '成功主题',
											message: "登陆成功",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
											url:"index"
					},
				]
			}
		},
		onShow() {
			if(getApp().globalData.cookie!=''){
				uni.navigateTo({
					url:"index"
				})
				return;
			}
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					//////console.log("admin:"+getApp().globalData.admin);
					this.op=res.data;
				}
			 });
			this.op=getApp().globalData.op;
		},
		methods: {
			findpassword(){
				uni.navigateTo({
					url:"findpassword"
				})
			},
			back(){
				uni.redirectTo({
					url:"index"
				})
			},
			register:function(){
				uni.navigateTo({
					url:"register"
				})
			},
			login:function(){
				if(!uni.$u.test.email(this.email)){
					this.$refs.uToast.show({
						...this.list[0],
						complete() {
							return;
						}
					})
				}
				if(this.password.length<7){
					this.$refs.uToast.show({
						...this.list[1],
						complete() {
							return;
						}
					})
				}
				var password=md5.hex_md5(this.password);
				uni.request({
					url:getApp().globalData.http+"/api/login_app",
					method:"POST",
					data:{
						"email":this.email,
						"password":password
					},
					success: (res) => {
						////console.log(res);	
						if(res.data.code==1001){
							getApp().globalData.username=res.data.data.username;
							getApp().globalData.userheadimage=res.data.data.userheadimage;
							getApp().globalData.userbackgroundimage=res.data.data.userbackgroundimage;
							getApp().globalData.cookie=res.data.data.cookie;
							getApp().globalData.sign=res.data.data.sign;
							getApp().globalData.save=res.data.data.save;
							getApp().globalData.bylike=res.data.data.bylike;
							getApp().globalData.registertime=res.data.data.registertime;
							getApp().globalData.userid=res.data.data.userid;
							getApp().globalData.admin=res.data.data.admin;
							//console.log(getApp().globalData.admin);
							uni.request({
								url:getApp().globalData.http+"/api/user_visit",
								method:"POST",
								data:{
									"userid":getApp().globalData.userid
								},
								success: (res) => {;
								}
							})
							uni.setStorage({
							    key: "admin",
							    data: getApp().globalData.admin,
							    success: function () {
							    }
							});
							uni.setStorage({
							    key: "sign",
							    data: getApp().globalData.sign,
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
							    key: "ban",
							    data: getApp().globalData.ban,
							    success: function () {
							    }
							});
							uni.setStorage({
							    key: "registertime",
							    data: getApp().globalData.registertime,
							    success: function () {
							    }
							});
							getApp().open();
							var id=20000000;
							if(getApp().globalData.replymessage.length>0){
								id=getApp().globalData.replymessage[0].id;
							}
							uni.request({
								url:getApp().globalData.http+"/api/getreplymessagenum",
								method:"POST",
								data:{
									"id":id,
									"userid":getApp().globalData.userid,
									"cookie":getApp().globalData.cookie
								},
								success:(res)=>{
									getApp().globalData.replymessagenum=res.data.num;	
									if(getApp().globalData.replymessagenum>0)
									{
									uni.request({
										url:getApp().globalData.http+"/api/getreplymessage",
										method:"POST",
										data:{
											"id":200000000,
											"userid":getApp().globalData.userid,
											"cookie":getApp().globalData.cookie
										},
										success:(res)=>{
											getApp().globalData.replymessage=res.data.reply;
												uni.setStorage({
												    key: "replymessage",
												    data: getApp().globalData.replymessage,
												    success: function () {
												    }
											});
										}
									})
									}
								}
							})
							uni.reLaunch({
								url:"index"
							})
						}
						else{
							this.$refs.uToast.show({
								...this.list[2],
								complete() {
									
								}
							})
						}
					},
					fail: (res) => {
						this.$refs.uToast.show({
							...this.list[4],
							complete() {
								
							}
						})
					}
				})

			}
		}
	}
</script>

<style>

</style>
