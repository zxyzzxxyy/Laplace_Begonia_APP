<template>
	<view style="background-color: #white;height:100vh;overflow-y: hidden;" id="a2">
		<!---->

		<!---->

		<view style="position: relative;display: flex;"
		>
		<view :class="{'a1':value==0,'a2':value!=0}" style="position: fixed;">	
			<themelist ref="themelist"></themelist>
		</view>
		
		<view  :class="{'a1':value==1,'a2':value!=1}" style="position: fixed;">
			<find  ref="find"></find>
		</view>
		
		<view  :class="{'a1':value==3,'a2':value!=3}" style="background-color:white;position: fixed;">
			<message ref="message" style="height:95vh"></message>
		</view>
		
		<view  :class="{'a1':value==4,'a2':value!=4}" >
			<myself ref="myself" v-if="skin==0" style="height:100vh;position: fixed;"></myself>
			<myself1 ref="myself"  v-if="skin!=0" style="height:100vh;position: fixed;"></myself1>
		</view>
		</view>
		<!---->
		<u-tabbar
			:fixed="true"
			:placeholder="false"
			:safeAreaInsetBottom="false"
			:activeColor="tabcolor"
			:inactiveColor="tabcolor2"
			:value="value"
			@change="change5"
			:customStyle="{color:'white'}"
			:buttons="button"
			:border="skin==0?true:false"
			v-if="!usesvga"
		>
			<u-tabbar-item text="频道"  @click="change4()">
				<image
					
					slot="inactive-icon"
					:src="bottomtar[0].image1"
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
				></image>
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="active-icon"
					:src="bottomtar[0].image2"
				></image>
			</u-tabbar-item>
			<u-tabbar-item text="探索" @click="findbacktop()">
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="inactive-icon"
					:src="bottomtar[1].image1"
				></image>
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="active-icon"
					:src="bottomtar[1].image2"
				></image>
			</u-tabbar-item>
			<u-tabbar-item text="" v-if="skin==0" >
				<view
					style="width:40px;height:40px;border-radius: 35%;
					display: flex;flex-direction: column;align-items: center;justify-content: center;
					"
					:style="{backgroundColor:color1}"
					slot="inactive-icon"
				>
					<view style="width:25px;height:25px;position: absolute;display: flex;align-items: center;justify-content: center;">
						<view style="width:25px;height:5px;border-radius: 15px;"
						:style="{backgroundColor:'white'}"
						>
							
						</view> 
					</view>
					<view style="width:25px;height:25px;position: absolute;display: flex;align-items: center;justify-content: center;">
					<view style="width:5px;height:25px;border-radius: 15px;;"
					:style="{backgroundColor:'white'}"
					>
					</view>
					</view>
				</view>
				<view
					style="width:30px;height:30px"
					slot="active-icon"
					
				>
				</view>
			</u-tabbar-item>
			
			<u-tabbar-item text="" v-if="skin!=0" >
				<view
					style="width:40px;height:40px;
					display: flex;flex-direction: column;align-items: center;justify-content: center;
					"
					slot="inactive-icon"
				>
					<image style="width:66px;height:50px;margin-top: -10px;" :src="newthemeicon" mode="aspectFit">
						
					</image>
				</view>
			</u-tabbar-item>
			
			<u-tabbar-item text="消息"  >
				<image
					:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="inactive-icon"
					:src="bottomtar[2].image1"
				></image>
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="active-icon"
					:src="bottomtar[2].image2"
				></image>
			</u-tabbar-item>
			<u-tabbar-item text="我的"  >
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="inactive-icon"
					:src="bottomtar[3].image1"
				></image>
				<image
						:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
					slot="active-icon"
					:src="bottomtar[3].image2"
				></image>
			</u-tabbar-item>
		</u-tabbar>
		
		<!---->
		<u-tabbar
			:fixed="true"
			:placeholder="false"
			:safeAreaInsetBottom="false"
			:activeColor="tabcolor"
			:inactiveColor="tabcolor2"
			:value="value"
			@change="change5"
			:customStyle="{color:'white'}"
			:buttons="button"
			:border="false"
			v-if="usesvga"
		>
			<u-tabbar-item text="频道"  @click="change4()">
				<image
					slot="inactive-icon"
					:src="bottomtar[0].image1"
					class='tabbar2'
				></image>
				<l-svga 
					style="width:55px;height:45px;margin-top: -15px;"
					slot="active-icon"
					:src="bottomtar[0].image2"
					>
				</l-svga>
			</u-tabbar-item>
			<u-tabbar-item text="探索" @click="findbacktop()">
				<image
					
					slot="inactive-icon"
					:src="bottomtar[1].image1"
					:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
				></image>
				
				<l-svga 
					
					slot="active-icon"
					:src="bottomtar[1].image2"
					style="width:55px;height:45px;margin-top: -15px;">
				</l-svga>
			</u-tabbar-item>
			<u-tabbar-item text="" v-if="skin==0" >
				<view
					style="width:40px;height:40px;border-radius: 35%;
					display: flex;flex-direction: column;align-items: center;justify-content: center;
					"
					:style="{backgroundColor:color1}"
					slot="inactive-icon"
				>
					<view style="width:25px;height:25px;position: absolute;display: flex;align-items: center;justify-content: center;">
						<view style="width:25px;height:5px;border-radius: 15px;"
						:style="{backgroundColor:'white'}"
						>
							
						</view> 
					</view>
					<view style="width:25px;height:25px;position: absolute;display: flex;align-items: center;justify-content: center;">
					<view style="width:5px;height:25px;border-radius: 15px;;"
					:style="{backgroundColor:'white'}"
					>
					</view>
					</view>
				</view>
				<view
					style="width:30px;height:30px"
					slot="active-icon"
					
				>
				</view>
			</u-tabbar-item>
			
			<u-tabbar-item text="" v-if="skin!=0" >
				<view
					style="width:40px;height:40px;
					display: flex;flex-direction: column;align-items: center;justify-content: center;
					"
					slot="inactive-icon"
				>
					<image style="width:66px;height:50px;margin-top: -10px;" :src="newthemeicon" mode="aspectFit">
						
					</image>
				</view>
			</u-tabbar-item>
			
			<u-tabbar-item text="消息"  >
				<image
				
					slot="inactive-icon"
					:src="bottomtar[2].image1"
					:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
				></image>
				
				<l-svga 
				
					slot="active-icon"
					:src="bottomtar[2].image2"
					style="width:55px;height:45px;margin-top: -15px;">
				</l-svga>
			</u-tabbar-item>
			<u-tabbar-item text="我的"  >
			<image
			
				slot="inactive-icon"
				:src="bottomtar[0].image1"
				:class="{'tabbar1':skinchoose==0,'tabbar2':skinchoose!=0}"
			></image>
			<l-svga 
				
				slot="active-icon"
				:src="bottomtar[3].image2"
			style="width:55px;height:45px;margin-top: -15px;">
			</l-svga>
			</u-tabbar-item>
		</u-tabbar>
		
		<!---->
		
		<u-toast ref="uToast"></u-toast>
		<view  style='height:100vh;width:100vw;z-index: 8;position: fixed' v-if="showpage==1">
			<view style="background: linear-gradient(to bottom right, rgb(124, 163, 255) , rgb(16, 216, 255));;height:100vh;width:100vw;display: flex;justify-content: center;
			background-attachment: fixed;background-position:center;
			display: flex;flex-direction: column;align-items: center;justify-content: center;	
			overflow: hidden;
			" :class="{'a3':op==2,'a4':op==1,'a5':op==0}"
			>
			<image :src="showback.url" style="width:100vw;height:100%;position: absolute;overflow-y: hidden;z-index: 9;"
			mode="aspectFill"	@load="loadover('success')" @error="loadover('error')"
			>
				<view style="width:100%;height:100%;;z-index: 9;"
				:style="{backgroundColor:skinchoose==0?'rgba(0,0,0,0.35)':'rgba(0,0,0,0)'}"
				>

				<view style="background-color: rgba(0,0,0,0.3);padding:5px 10px 5px 10px;border-radius:15px;z-index: 8;position: absolute;font-size: 14px;color:white;margin-left: 80%;margin-top: 10%;display: flex;flex-direction: row;">
					<text @click="delete1()">跳过</text> 
					<u-count-down ref="countDown" :time="4000" format="HH:mm:ss" :autoStart="star" @change="changetime" style="margin-left: 10px;">
						<view >
						    <view >
						        <text style="font-size: 14px;color:white;">{{timeData}}</text>
						    </view>						        
						</view>
					</u-count-down>
				</view>
				<view style="z-index: 8;width:100%;height:100%;display: flex;align-items: center;justify-content: center;"
				v-if="skin==0"
				>
					<text style="font-size: 50px;color:white;text-shadow: 3px 3px black;margin-top: -20vh;">学伴 WMU</text>
				</view>
				<view style="z-index: 8;bottom:10px;position: absolute;font-size: 12px;color:white;margin-left: 3%;" v-if="skin==0">
					 <view  v-if="showback.pid!=null">{{showback.title}} <br> pid:{{showback.pid}} <br> 画师：{{showback.username}}</view>
				</view>
				<view style="z-index: 8;bottom:10px;position: absolute;font-size: 12px;color:white;margin-left: 3%;" v-if="skin!=0">
					 <view :style="{color:color3}">{{tips}}</view>
				</view>
				</view>
				</image>
			</view>
		</view>
	</view>
</template>
<style>
.a2{
	z-index: -1;
	opacity: 0;
	transition: 0.3s;
}
.a1{
	z-index: 1;
	opacity: 1;
	transition: 0.3s;
},
.a4{
		z-index: 8;
		opacity: 0;
		transition: 0.3s;
	}
.a3{
		z-index: 8;
		opacity: 1;
		transition: 0.3s;
	}
.a5{
		z-index: -1;
		opacity: 0;
		display: none;
	}
.tabbar1{
	width:30px;
	height:30px;
}	
.tabbar2{
	width:55px;
	height:45px;
	margin-top: -15px;
}
</style>
<script>
	import showpage from "@/pages/index/show.vue"
	import myself from"@/pages/index/myself.vue" 
	import myself1 from"@/pages/index/myself1.vue" 
	import find from"@/pages/index/find.vue"
	import message from"@/pages/index/message.vue"
	import userhead from "@/pages/index/userhead/userhead.vue"
	import themelist from "@/pages/index/themelist.vue"
	export default {
		components:{
			myself,find,message,userhead,themelist,showpage,myself1
		},
		data() {
			return {
				value:0,
				page:0,
				color1:"#ff007f",
				color2:"white",
				list1:[
				],
				tabcolor:"#7d7e80",
				timeData:3,
				colors:"#fff",
				status:"loading",
				keyword:"",
				show:1,
				skinchoose:0,
				showpage:1,
				type:0,
				star:false,
				limit:0,
				scrollTop:0,
				themelist:[],
				leftlist:[],
				mylike:[],
				screenwidth:0,
				tips:"",
				fenlei:"全部分类",
				button:"",
				tabcolor2:"black",
				screenwidth1:0,
				h1:0,
				h2:0,
				current:0,
				current1:false,
				color3:"white",
				top:0,
				list:[
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "请登录",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
				],
				setWidth:0,
				setWidth1:0,
				jugelogin:false,
				showback:{},
				usesvga:false,
				op:2,
				skin:0,
				bottomtar:[
				{
					image1:"/static/shouye.png",
					image2:"/static/shouye (1).png",
				},
				{
					image1:"/static/huore.png",
					image2:"/static/huore (1).png",
				},
				{
					image1:"/static/xiaoxi.png",
					image2:"/static/xiaoxi (1).png",
				},
				{
					image1:"/static/wode.png",
					image2:"/static/wode (1).png",
				},
				],
			}
		},
		onShow() {
			this.showpage=getApp().globalData.showpage;
			getApp().globalData.showpage=0;
			if(getApp().globalData.cookie!=''){
				 this.jugelogin=true;
			}
			
			setTimeout(() => {
				this.$refs.themelist.tuijian();
			}
			, 100)
			if(this.value==4){
				this.$refs.myself.getmyself();
			}
			if(getApp().globalData.cookie!='')
			uni.request({
				url:getApp().globalData.http+"/api/jugeuser",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie
				},
				success: (res) => {
					if(res.data.code==1002){
						uni.showToast({
							title:"其它设备登录",
							icon:"error"
						})
						getApp().globalData.username='';
						getApp().globalData.userheadimage='';
						getApp().globalData.userbackgroundimage='';
						getApp().globalData.cookie='';
						getApp().globalData.sign='';
						getApp().globalData.save='';
						getApp().globalData.bylike='';
						getApp().globalData.registertime='';
						getApp().globalData.userid='';
						getApp().globalData.admin=0;
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
						setTimeout(() => {
							uni.reLaunch({
								url:"index"
							})
						}
						, 1000)
						
					
					}
					}
				
			})
		},
		mounted(){
			uni.getStorage({
			    key:"skinchoose",
			    success: function(res){
			        getApp().globalData.skinchoose=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
getApp().globalData.showpage=0;
			getApp().globalData.showpage=0;	
			this.skin=getApp().globalData.skinchoose;
			if(getApp().globalData.skinchoose==0){
			this.showpageonload();
		
			}
			else{
				this.color3=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.skinchoose=getApp().globalData.skinchoose;
				this.colors=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.showback.url=getApp().globalData.skin[getApp().globalData.skinchoose-1].starimage;
				this.tips=getApp().globalData.skin[getApp().globalData.skinchoose-1].tip1;
				this.newthemeicon=getApp().globalData.skin[getApp().globalData.skinchoose-1].newthemeicon;
				this.bottomtar=getApp().globalData.skin[getApp().globalData.skinchoose-1].bottomtar;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor1;
				this.color2=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.tabcolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].selectcolor;
				this.tabcolor2=getApp().globalData.skin[getApp().globalData.skinchoose-1].unselectcolor;
				this.button=getApp().globalData.skin[getApp().globalData.skinchoose-1].button;
				this.usesvga=getApp().globalData.skin[getApp().globalData.skinchoose-1].usesvga;
				if(getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor=='white')
				uni.setNavigationBarColor({
					frontColor:"#ffffff",
					backgroundColor:''
				})
				else
				uni.setNavigationBarColor({
					frontColor:"#000000",
					backgroundColor:''
				})
				this.stop2(2);
				
			}
			let that = this;
			
			if(getApp().globalData.cookie!='')
				this.jugelogin=true;
			uni.onTabBarMidButtonTap(()=>{
				if(that.jugelogin)
				uni.navigateTo({
					url:"/pages/index/newtheme"
				})
				else ;
			})
			
			
		},
		methods: {
			changetime(e){
				this.timeData=e.seconds;
			
			},
			stop2(e){
				uni.$u.throttle(this.stop1(e), 10000);
				
			},
			loadover(e){
				let _this=this;
				setTimeout(()=>{
					plus.navigator.closeSplashscreen();	
					_this.$refs.countDown.start();
				},100);
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
						_this.changeshowpage();
					 }, 300);
					
				},3000)
				}
			},
			delete1(){
				this.op=1;
				let _this=this;
				setTimeout(function() {
					getApp().globalData.showpage=0;
					_this.op=0;
					_this.changeshowpage();
					}
				, 300);
			},
			showpageonload(){
				{
					let _this =this;
					setTimeout(function() {
					    {
							
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
									
										var temp1="";
										/*pathToBase64(getApp().globalData.pixiv[i].url)
										  .then(base64 => {
											console.log(base64);
											temp1=base64;
										})*/
										this.showback.url=getApp().globalData.pixiv[i].url+'?imageMogr2/thumbnail/2000000@';
									
								
										_this.e=null;
						
										 return;
									}
								}
								if(sub==-1){
									uni.downloadFile({
										url: url, 
											success: (res) => {
											
												if (res.statusCode === 200) {
													
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
			changeshowpage(e){
				this.showpage=getApp().globalData.showpage;
			},
			findbacktop(){
				
					if(this.page==1){
						this.$refs.find.backtop();
					}
			},		
			login(){
				uni.navigateTo({
					url:"login"
				})
			},
			change4(){
				if(!this.current1){
					this.$refs.themelist.change4();
					this.$refs.themelist.tuijian();
				}
			},
			change5(name) {
				if ((getApp().globalData.cookie=='')&&(name === 3|| name ===2 || name ===4)) return this.login()
				else if(name==2){
					uni.navigateTo({
						url:"/pages/index/newtheme"
					})
				}
				else if(name==0){
					this.value=0;
					if(this.current1)
						setTimeout(() => {
							 this.current1=false;
							 this.page=0;
						}, 10)
				}
				else if(name==1){
					this.value=1;
					this.current1=true;
					setTimeout(() => {
						 this.page=1;
					}, 10)
				}else if(name==3){
					this.value=3;
					this.current1=true;
					 this.page=0;
				}
				else if(name==4){
					this.value=4;
					this.current1=true;
					this.page=0;
				}
			
				/*else if(name ==0 ){
				let old = this.page;
				this.page=old;
				 this.$nextTick(function() {
				    this.page = name
				});
				}
				else if(name ==1){
				let old = this.page;
				this.page=old;
				 this.$nextTick(function() {
				    this.page = name
				});
				
				this.$refs.find.load();
					
				}
				else if(name ==3 ){
				let old = this.page;
				this.page=old;
				 this.$nextTick(function() {
				    this.page = 2
				});
				this.page = 2	
				}
				else if(name ==4){
				let old = this.page;
				this.page=old;
				 this.$nextTick(function() {
				    this.page = 3
				});
				this.$refs.myself.getmyself();
				};
				setTimeout(() => { 	
				if(name == 0)
				this.current1=false;
				else{
					this.current1=true;
				}
				}, 10)
	*/
			},
			
			
		
		}
	}
</script>


