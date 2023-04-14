<template>
	<view style="display: flex;justify-content;: center;flex-direction:column;align-items:center;justify-content:center;height:50vh">
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
				 style="font-weight: 700;"></text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:15px">
			1
		</view>
		<view style="width: 80vw;">
		<u--input
		  placeholder="请输入邮箱"
		  clearable
							style=";margin-top:20px;margin-bottom: 40px;"
							v-model="email"
							
		></u--input>
		<u-button type="primary" text="确认" size="18"
			@click="sendemail"
		></u-button>
		</view>
		<view>
				<u-toast ref="uToast"></u-toast>
		
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				email:"",
				color:"white",
				color1:"black",
				list:[
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "邮箱未注册",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "邮箱格式错误",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
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
			sendemail:function(){
				if(!uni.$u.test.email(this.email)){
					this.$refs.uToast.show({
						...this.list[1],
						complete() {
							
						}
					})
					return;
				}
				uni.request({
					url:getApp().globalData.http+"/api/sendemail",
					method:"POST",
					data:{
						"email":this.email
					},
					success:(res)=>{
						if(res.data.code==1001){
							uni.navigateTo({
								url:"findpassword1?email="+this.email
							})
						}
						else{
							this.$refs.uToast.show({
								...this.list[0],
								complete() {
									
								}
							})
						}
					}
				})
			}
		}
	}
</script>

<style>

</style>
