<template>
	<view style="display: flex;justify-content;: center;flex-direction:column;align-items:center">
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
				 style="font-weight: 700;">修改密码</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:15px">
			1
		</view>
		<view style="width: 80vw;">
		<u--input
		  placeholder="请输入旧密码"
		  clearable
							style=";margin-top:20px;margin-bottom: 40px;"
							v-model="oldpassword"
							
		></u--input>
		</view>
		<view style="width: 80vw;">
		<u--input
		  placeholder="请输入新密码"
		  clearable
							style=";margin-top:20px;margin-bottom: 40px;"
							v-model="password"
							
		></u--input>
		</view>
		<view style="width: 80vw;">
		<u--input
		  placeholder="请确认新密码"
		  clearable
							style=";margin-top:20px;margin-bottom: 40px;"
							v-model="repassword"
							
		></u--input>
		</view>
		<view style="width: 80vw;">
		<u-button type="primary" text="修改" size="18"
		@click="changepassword()"
		></u-button>
		</view>
		<view>
				<u-toast ref="uToast"></u-toast>
		
		</view>
	</view>
</template>

<script>
	import md5 from '@/pages/md5.js'
	export default {
		data() {
			return {
				oldpassword:"",
				color:"white",
				color1:"black",
				password:"",
				repassword:"",
				list:[
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "两次输入的密码不一致",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message:"密码长度小于七位",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message:"修改失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'success',
						icon: false,
						title: '成功主题',
						message:"修改成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
				]
			}
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
		methods: {
			back(){
				uni.navigateBack();
			},
			changepassword:function(){
				if(this.password!=this.repassword){
					this.$refs.uToast.show({
						...this.list[0],
						complete() {
							
						}
					})
					return;
				}
				else if(this.password.length<7){
					this.$refs.uToast.show({
						...this.list[1],
						complete() {
							
						}
					})
					return;
				}
				else if(this.oldpassword.length<7){
					this.$refs.uToast.show({
						...this.list[1],
						complete() {
							
						}
					})
					return;
				}
				var password=md5.hex_md5(this.password);
				var oldpassword=md5.hex_md5(this.oldpassword);
				uni.request({
					url:getApp().globalData.http+"/api/changepassword",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"password":password,
						"oldpassword":oldpassword,
						"userid":getApp().globalData.userid
					},
					success:(res)=>{
				
						if(res.data.code==1001){
							this.$refs.uToast.show({
								...this.list[3],
								complete() {
									
								}
							})
							setTimeout(() => {  
								uni.reLaunch({
									url:"index"
								})
							}, 1010)

						}else{
							this.$refs.uToast.show({
								...this.list[2],
								complete() {
									
								}
							})
						}
					},
					fail:(res)=>{
						this.$refs.uToast.show({
							...this.list[2],
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
