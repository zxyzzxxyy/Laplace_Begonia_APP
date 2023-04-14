<template>
	<view style="position: relative;;font-size: 16px;width: 100vw;background-color: #efefef;"
	
	>
		<view style="position: fixed;height:50px;background-color: white;display: flex;align-items: center;z-index: 2;padding-top:2rem;float:left"
			:style="{backgroundColor:color}"
		>
			<u-icon size="25" name="arrow-left" @click="back" :color="color1"></u-icon>
			<view style="display:flex;justify-content: center;width:100vw;align-items:center;margin-left: -25px;"
			:style="{color:color1}"
			>
			<text style="font-size: 18px;"
			
			>{{username}}</text>
			
			</view>
		</view>

		<view style="min-height: 90vh;height:auto;padding-top:5rem;padding-bottom:50rpx;background-color: #efefef;padding-bottom: 80px;" scroll-y="true" :scroll-top="top" :scroll-with-animation="true" 
		@refresherrefresh="getmore()" :refresher-triggered="abc" :refresher-enabled="true"	@refresherrestore="abcd()" refresher-background="#efefef">
			<view v-for="(item,index) in chatlist" :class="{'a1':show==0,'a2':show==1}" style="margin-bottom: px;"
			:id="'a'+item.id">
				<view style="width:100vw;display: flex;align-items: center;font-size: 12px;color:#909399;justify-content: center;margin-top: 5px;" v-if="juge1(index)&&juge3(item)">{{time1(item.time)}}</view>
				<view v-if="juge(item)&&juge3(item)" style="width:98vw;margin-right: 2vw;margin-top: 5px;margin-bottom: 5px;display: flex;flex-direction: row; align-items: flex-start"
				 @longpress="test(item)"
				>
				
					<view style="width:auto;border-radius: 5px;background-color: #3c9cff;overflow: hidden;max-width: 50vw;padding:7px;padding-left:10px ;margin-left: auto;margin-top: 10px;">
						<text style="border-radius: 5px;font-size: 16px;color:#ffffff;">{{item.message}}</text>
						<view v-if="jugeimage(item.image)" style="margin-top: 5px;">
							<image :src="item.image" style="min-width: 50px;height:auto;max-width: 100%;border-radius: 5px;"  mode="widthFix"
							@load="bottom1"
							></image>
						</view>
					</view>
				<view style="width:50px;margin-left: 8px;">
					<u-avatar mode="aspectFill":src="myuserheadimage" v-if="myuserheadimage!=null" size="45"></u-avatar>
					<u-avatar :text="myuserheadimage.substr(0,1)"  randomBgColor v-if="myuserheadimage==null" size="45"></u-avatar>

				</view>
				</view>
				<view v-if="!juge(item)&&juge3(item)" style="width:98vw;margin-right: 2vw;margin-top: 5px;margin-bottom: 5px;display: flex;flex-direction: row; align-items: flex-start"
				@longpress="test2(item)"
				>
				
				<view style="width:50px;margin-left: 8px;">
					<u-avatar mode="aspectFill":src="userheadimage" v-if="userheadimage!=null" size="45"></u-avatar>
					<u-avatar :text="username.substr(0,1)"  randomBgColor v-if="userheadimage==null" size="45"></u-avatar>
				
				</view>
				<view style="width:auto;border-radius: 5px;background-color: #ffffff;overflow: hidden;max-width: 50vw;padding:7px;padding-right:10px ;margin-top: 10px;">
					<text style="border-radius: 5px;font-size: 16px;color:#000000;">{{item.message}}</text>
					<view v-if="jugeimage(item.image)" style="margin-top: 5px;">
						<image :src="item.image" style="min-width: 50px;height:auto;max-width: 100%;border-radius: 5px;"  mode="widthFix"></image>
					</view>
				</view>
				</view>
			</view>
		</view>
		<view style="height:3rem;background-color: #f5f5f5;width:100vw;display:flex;align-items:center;flex-direction:row;padding-bottom:1vh;padding-top:1vh;bottom:0;position:fixed">
			
			 <input
			    placeholder="请输入内容"
			    border="surround"
			    v-model="message"
				auto-blur
				 :adjust-position="true"
				:confirmHold="true"
				:holdKeyboard="true"
				@confirm="send()"
				@focus="jianpan()"
				@blur="blur()"
				style="background-color: white;width:63%;max-height:80%;margin-left:10px;border-radius:100px;font-size:16px;padding-left:1rem;padding-right:1rem;padding-top:0.5rem;padding-bottom:0.5rem"
			  ></input>
			
			  <button type="primary" style="width:15%;border-radius: 100px;height:80%;padding-top:1px;padding-bottom:1px;color:white;font-size:15px;min-width: 60px;margin-left:5px;margin-right: 4px;" @touchend.prevent="send" >发送</button>
			  <view style="margin-right: 1%;display: flex;align-items: center;justify-content: center"  v-if="image!=''" @click="image=''">
				<u-icon name="photo" color="#2979ff" size="28"></u-icon>
			  </view>
			  <view style="margin-right: 1%;" v-if="image==''" @click="head()">
			  <u-icon name="photo" size="28"></u-icon>
			  </view>
		</view>
		<u-action-sheet :actions="list"  :show="show1" @close="show1=false,item=[]" @select="test1"></u-action-sheet>
        <u-action-sheet :actions="list2"  :show="show2" @close="show2=false,item=[]" @select="test1"></u-action-sheet>
        			
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[
					{
						name:'删除',
					},
					{
						name:'撤回'
					}
				],
				list2:[
					{
						name:'删除',
					}
				],
				userid:0,
				username:"123",
				userheadimage:"",
				color:"white",
				color1:"black",
				myuserheadimage:"",
				message:"",
				image:"",
				chatlist:[],
				chatlist1:[],
				value:"",
				sub:0,
				show:0,
				show1:false,
				show2:false,
				timer: null,
				top:0,
				f:true,
				bottom:0,
				height1:0,
				height2:0,
				abc:false,
				juge2:0,
				i:0,
				j:0,
				sub1:0,
				item:[],
				list1:[
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "撤回时间超过两分钟",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					}
				]
			}
		},
		onLoad(res){
			let that=this;

			this.userid=res.userid;
			this.username=res.username;
			this.userheadimage=res.userheadimage;
			this.myuserheadimage=getApp().globalData.userheadimage;
			if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
			}
			uni.setNavigationBarTitle({
				title:this.username
			})
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
			for(var i=0;i<getApp().globalData.chatlist.length;i++){
				if(getApp().globalData.chatlist[i].a==this.userid||getApp().globalData.chatlist[i].b==this.userid)
				this.chatlist1.push(getApp().globalData.chatlist[i]);
			}
			var i=0;
			if(this.chatlist1.length>=10){
				this.i=this.chatlist1.length-10;
				this.j=i;
			}
			else {
				this.i=0;
				this.j=i;
			}
			for(this.i;this.i<this.chatlist1.length;this.i++){
				if(this.chatlist1[this.i].a==this.userid||this.chatlist1[this.i].b==this.userid)
				this.chatlist.push(this.chatlist1[this.i]);
			}
			this.j++;
			this.sub=getApp().globalData.chatlist.length-1;
			this.top=9999999999;
			
			setTimeout( () => {
				this.show=1;
			}, 500)
			this.timer = setInterval( () => {
				this.add();// 业务逻辑	
			}, 500)
		},
		onPageScroll(e){
			if(e.scrollTop<5){
				this.getmore();
			}
		},
		methods: {
			bottom1(){
				
			},
			setPageScrollTo(selector){
			
				let view = uni.createSelectorQuery().in(this).select(selector);
				view.boundingClientRect((res) => {
					//console.log()
					//console.log(res);
					uni.pageScrollTo({
					    scrollTop:res.top-100,	// -30 为多显示出大半个消息的高度，示意上面还有信息。
					    duration: 50
					});
				}).exec();
			},
			juge3(e){
				if(e.time==0)return false;return true;
			},
			test1(e){
				//console.log(e.name);
				//console.log(this.item);
				if(e.name=="撤回"){
					var time1=parseInt(this.item.time);
					var time2= new Date()/1000;
					time2=parseInt(time2);
					//console.log(time1+" "+time2);
					if(time2>time1+2*60){
						//console.log("123");
						this.$refs.uToast.show({
							...this.list1[0],
							complete() {
								return;
							}
						})
						return;
					}
					else{
						//console.log("456");
						this.backmessage(this.item);
					}
				}
				else if(e.name=="删除"){
					for(var i=0;i<getApp().globalData.chatlist.length;i++){
						if(getApp().globalData.chatlist[i].id==this.item.id){
							getApp().globalData.chatlist[i].time=0;
							uni.setStorage({
							    key: "chatlist",
							    data: getApp().globalData.chatlist,
							    success: function () {
							    } 
							});
							break;
						}
					}
					for(var i=0;i<this.chatlist.length;i++){
						if(this.chatlist[i].id==this.item.id){
							this.chatlist[i].time=0;

						}
					}
				}
			},
			test(e){
				this.show1=true;
				this.item=e;
			},
			test2(e){
				this.show2=true;
				this.item=e;
			},
			backmessage:function(e){
			//	console.log(e);
				(getApp().send(e.a,e.b,e.id,e.time,"back"));
	
			},
			abcd(){
				this.abc=false;
			
			},
			getmore:function(){
				if(this.abc==true)return;this.abc = true;
				//console.log("123");
				setTimeout(() => {	this.abc=false;},1300)
				 setTimeout(() => {
					 var x=0;
					 if(this.chatlist1.length-this.j*10>=10){
					 	x=this.chatlist1.length-this.j*10
					 	this.j++;
					
					 }
					 else if(this.chatlist1.length-this.j*10<10&&this.chatlist1.length-this.j*10>0){
					 	x=this.chatlist1.length-this.j*10;
					
					 	this.j++;
					 }
					 else{
						 this.j++;
					 
					 	return;
					 }
					 this.i=x;
					var selector='#a'+this.chatlist[0].id;
					 for(var t=10;t>0;this.i--,t--){
					 	if(this.chatlist1[this.i].a==this.userid||this.chatlist1[this.i].b==this.userid)
					 	this.chatlist.unshift(this.chatlist1[this.i]);
					 }
					this.$nextTick(()=>{
					this.setPageScrollTo(selector);
					});
				}, 1000)
			},
			blur:function(){
				this.bottom=0;
			},
			jianpan:function(e){
				
			},
			jugeimage:function(e){
			
				if(e.length==0)return false;
				return true;
			},
			juge1:function(i){
			
				if(i==0)return true;
				if(this.chatlist[i].time-this.chatlist[i-1].time>60)return true;return false;
			},
			add:function(){
				if(this.sub!=getApp().globalData.chatlist.length-1){
					for(var i=this.sub+1;i<getApp().globalData.chatlist.length;i++){
						
						var temp=JSON.parse(JSON.stringify(getApp().globalData.chatlist[i]));
						if(temp.b==this.userid||temp.a==this.userid)
						this.chatlist.push(temp);
						
					}
					this.sub=getApp().globalData.chatlist.length-1;
					
					setTimeout( () => {
					uni.pageScrollTo({
					    scrollTop:999999999 ,	
						duration: 100
					});
					}, 100)
				}
				for(this.sub1;this.sub1<getApp().globalData.chatlistback.length;this.sub1++){
					for(var i=0;i<this.chatlist.length;i++){
					
						if(this.chatlist[i].id==getApp().globalData.chatlistback[this.sub1]){
						
							this.chatlist.splice(i,1);
							break;
						}
					}
				}
			},
				
			back:function(){
				uni.navigateBack({
					
				})
			},
			juge:function(res){
				if(res.a==getApp().globalData.userid)return true;return false;
			},
			send:function(){
				
				if(this.message==''&&this.image=='')return;
				(getApp().send(getApp().globalData.userid,this.userid,this.message,this.image,"message"));
				this.message="";
				this.image="";
			},
			head:function(){
				let that = this;
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
									that.image=res.data.location;

							}
						})
					}
				});
			},
			time1:function(e){
			
				var g = new Date();
				var e1 = new Date(e*1000);
				var data=g.getDate();
				var data1=e1.getDate();
				if(data==data1){
					let date = new Date(e*1000);
					let h = date.getHours();
					let m = date.getMinutes();
					if(m<10)
					m="0"+m;
					return h+":"+m
				}
				else{
					var g = new Date().getTime();
					var d = new Date(g);
					var e = new Date(e*1000);
					var year = d.getFullYear(); 
					var month = d.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date = d.getDate(); 
					var year1 = e.getFullYear();
					var month1 = e.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date1 = e.getDate(); 
					var h = e.getHours();
					var m = e.getMinutes();
					if(m<10)
					m="0"+m;
					if(year!=year1)
						return year1+"-"+month1+"-"+date1+" "+h+":"+m;
					else return month1+"-"+date1+" "+h+":"+m;
				}
			},
		}
	}
</script>

<style>
.a1{
	opacity: 0;
}
.a2{
	opacity: 1;
}
</style>
