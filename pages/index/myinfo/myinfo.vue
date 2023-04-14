<template>
	<view style="background-color: #f4f5f5;height:100vh;overflow-y: hidden;">
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
				 style="font-weight: 700;">我的信息</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px">
			1
		</view>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:80px;align-items: center;background-color: white;
		" @click="head()">
			<view>
				<text>头像</text>
			</view>
			<view style="margin-left: auto;" >
				<u-avatar mode="aspectFill" :src="userheadimage" v-if="userheadimage!=''" size="45"></u-avatar>
				<u-avatar :text="username.substr(0,1)"  randomBgColor v-if="userheadimage==''" size="45"></u-avatar>
			</view>
			<view style="height:50px;display: flex;align-items: center;;margin-left:5px" >
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<u-divider style="margin-top:0;margin-bottom: 0;"></u-divider>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		">
			<view>
				<text>昵称</text>
			</view>
			<view style="margin-left: auto;color:#909399">
				<text>{{username}}</text>
			</view>
			<view style="height:50px;display: flex;align-items: center;;margin-left:5px">
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<u-divider style="margin-top:0;margin-bottom: 0;"></u-divider>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		" @click="opentime()">
			<view >
				<text>出生年月</text>
			</view>
			<view style="margin-left: auto;color:#909399" >
				<text>{{birthday}}</text>
			</view>
			<view style="height:50px;display: flex;align-items: center;;margin-left:5px">
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<u-divider style="margin-top:0;margin-bottom: 0;"></u-divider>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		"  @click="open()">
			<view style="width:20%">
				<text>签名</text>
			</view>
			
			<view style="margin-left: auto;" >
				<u--text :text="sign" lines="1" color="#909399"></u--text>
			</view>
			<view style="height:50px;display: flex;align-items: center;margin-left:5px"  >
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<u-divider style="margin-top:0;margin-bottom: 0;"></u-divider>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		" @click="toshenfen">
			<view style="width:20%">
				<text>身份标识</text>
			</view>
			
			<view style="margin-left: auto;" >
				<u--text :text="shenfen" lines="1" color="#909399"></u--text>
			</view>
			<view style="height:50px;display: flex;align-items: center;margin-left:5px"  >
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<!---->
		<view style="height:15px;width:100vw;background-color: #f4f5f5;">
			
		</view>
		<!---->
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		"  @click="setheadborder()">
			<view style="width:20%">
				<text>头像框</text>
			</view>
			<view style="height:50px;display: flex;align-items: center;margin-left:auto">
				<u-icon name="arrow-right" color="#82868b" size="22"></u-icon>
			</view>
		</view>
		<!---->
		<view style="height:15px;width:100vw;background-color: #f4f5f5;">
			
		</view>
		<!---->
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		">
			<view style="width:20%">
				<text>UID</text>
			</view>
			<view style="margin-left: auto;color:#909399">
				<text>{{userid}}</text>
			</view>
		</view>
		<u-divider style="margin-top:0;margin-bottom: 0;"></u-divider>
		<view style="width:96vw;padding-left: 2vw;padding-right: 2vw;display: flex;flex-direction: row;
		height:50px;align-items: center;;background-color: white;
		">
			<view style="width:20%">
				<text>注册日期</text>
			</view>
			<view style="margin-left: auto;color:#909399">
				<text>{{time2(registertime)}}</text>
			</view>
		</view>
		<!---->
		<view style="height:100vh;width:100vw;background-color: #f4f5f5;">
			
		</view>
		<!---->
		<uni-popup ref="popup" type="dialog">
		    <uni-popup-dialog mode="input" placeholder="请输入签名内容" type="success" :duration="2000" :before-close="true" @close="close" @confirm="confirm"></uni-popup-dialog>
		</uni-popup>
		<gpp-date-picker @onCancel="closetime" @onConfirm="setbirthday" ref="times" :endDate="endDate">
		    {{pickerDate}}
		</gpp-date-picker>
		<u-toast ref="uToast"></u-toast>

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
				userid:0,
				username:"",
				userheadimage:"",
				sign:"",
				color:"white",
				color1:"black",
				birthday:0,
				registertime:0,
				show:false,
				show1:false,
				show2:false,
				birthday:"",
				endDate:"",
				pickerDate:"",
				shenfen:"",
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
		onShow(){
			this.getmyself();
		},
		methods: {
			back(){
				uni.navigateBack();
			},
			time2:function(e){
				var d = new Date(e*1000);
				var year = d.getFullYear();
				var month = d.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
				var date = d.getDate(); 
				return year+"-"+month+"-"+date;
			},
			head:function(){
				let that=this;
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
									url:getApp().globalData.http+"/api/setuserheadimage",
									method:"POST",
									data:{
										"userheadimage":res.data.location,
										"userid":getApp().globalData.userid,
										"cookie":getApp().globalData.cookie
									},
									success: (res1) => {
										if(res1.data.code==1001){
											getApp().globalData.userheadimage=res.data.location;
											that.userheadimage=getApp().globalData.userheadimage;
											uni.setStorage({
											    key: "userheadimage",
											    data: getApp().globalData.userheadimage,
											    success: function () {
											    }
											});			
											that.getmyself();
										}
										else{
											that.$refs.uToast.show({
												...that.upload[1],
												complete() {
													return;
												}
											})
										}
									},
									fail:(res)=>{
										that.$refs.uToast.show({
											...that.upload[1],
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
				this.$refs.times.show();
			},
			closetime(){
				this.$refs.times.hide();
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
							this.getmyself();
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
			toshenfen(){
				uni.navigateTo({
					url:"/pages/index/shenfen"
				})
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
			getmyself(){
				uni.request({
					url:getApp().globalData.http+"/api/getmyself",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie
					},
					success: (res) => {
						this.birthday=res.data.data.birthday;
						if(this.birthday!=null){
							let date = new Date(parseInt(this.birthday)*1000);
							        let y = date.getFullYear();
							        let MM = date.getMonth() + 1;
							        MM = MM < 10 ? "0" + MM : MM;
							        let d = date.getDate();
							        d = d < 10 ? "0" + d : d;
							      
							        var dayDate = y + "-" + MM + "-" + d;
							this.birthday=dayDate;
						}
						this.userid=res.data.data.userid;
						this.username=res.data.data.username;
						this.userheadimage=res.data.data.userheadimage;
						this.userbackgroundimage=res.data.data.userbackgroundimage;
						this.sign=res.data.data.sign;
						this.save=res.data.data.save;
						this.bylike=res.data.data.bylike;
						this.registertime=res.data.data.registertime;
						this.admin=res.data.data.admin;
						this.email=res.data.data.email;
						this.toutu=res.data.data.toutu;
						this.attention=res.data.data.attention;
						this.fans=res.data.data.fans;
						this.ban=res.data.data.ban;
						this.show=true;
						this.shenfen=res.data.shenfen;
						var temp="";
						for(var i=0;i<this.shenfen.length;i++){
							temp+=this.shenfen[i].name;
							if(i+1!=this.shenfen.length)temp+="、";
						}
						this.shenfen=temp;
						this.pianyi=res.data.data.pianyi;
						this.headborder=res.data.data.headborder;
						this.bantime=res.data.data.ban_time;
						this.banreason=res.data.data.banreason;
						var i="";
						for(var j=0;j<this.email.indexOf("@")-4;j++)i=i+'x';
						this.email=this.email.substring(0,3)+i+this.email.substring(this.email.indexOf("@")-1,this.email.length);
					}
				})
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
			var nowDate = new Date();
			     var date = {
			       year: nowDate.getFullYear(),
			       month: nowDate.getMonth() + 1,
			       day: nowDate.getDate(),
			     }
			     var dayDate = date.year + '-' + (date.month >= 10 ? date.month : '0' + date.month) + '-' + (date.day >= 10 ? date.day : '0' + date.day);
							  this.endDate=dayDate;
			this.getmyself();
		}
	}
</script>

<style>

</style>
