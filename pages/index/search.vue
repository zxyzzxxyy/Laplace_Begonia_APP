<template>
<view style="background-color: white;;width:100vw;;background-size: cover;background-attachment: fixed;display: flex;;" v-bind:style="{backgroundImage:'url(' + userbackgroundimage + ')'}">
		<!--顶部栏-->
		<!---->
		<scroll-view style="background-color: white;width:100%;height:100vh;display: flex;flex-direction: column;align-items: center;justify-content: center;;display: flex;justify-content: center;" scroll-y @scrolltolower="getmoretheme">
			<view style=";width:100vw;;display: flex;flex-direction: column;align-items: center;overflow-x: hidden;"
			>
				<view style=";padding-top: 4.5vh;;height:35px;margin-bottom:10px;width:100%;display: flex;flex-direction: row;align-items: center;justify-content: center;padding-bottom: 10px;"
					:style="{backgroundColor:color1}"
				>
					<view style=";margin-left: 0%;width:84%;border:0px solid #f3f4f6;height:35px;display: flex;border-radius: 5px;
					border-radius: 15px;
					background-color: #f3f4f6;
					">
					 <input
						placeholder="要搜点什么..."
						v-model="key"
						 @confirm="search"
						type="text"
						style="border:none;margin-left: 15px;min-height:35px;width:100%;background-color: #f3f4f6;"
						:adjust-position="false"
					  />
					  <u-icon name="search" color="#909399" size="28" style="margin-left: auto;margin-right: 5px;" @click="search()"></u-icon>
					</view>
					<view style="margin-left: 3%;" @click="back()">
						<u-icon name="close" size="20"
						:color="color2"
						></u-icon>
					</view>
				</view>
				<!---->
				<view style="font-size: 15px;;font-weight: 800;margin-left: 2.5vw;display: flex;align-items: center;width:95vw;flex-wrap: wrap;margin-top: 10px;"
				v-if="show2&&hotsearchlist.length>0"
				>
					<view style="display: flex;flex-direction: row;align-items: center;">
						<image src="../../static/hot.png" style="width:20px;height:20px;margin-right: 5px;"></image>
						<text>热门搜索</text>
					</view>
				</view>
				<view style="margin-left: 2.5vw;display: flex;align-items: center;width:95vw;flex-wrap: wrap;"
				v-if="show2"
				>
					
					<view v-for="(item,index) in hotsearchlist" style="color:#0088ff;font-size: 15px;;background-color: #e4f4ff;border-radius: 5px;padding:4px;padding-left:6px;padding-right: 6px;margin-right: 10px;margin-top: 10px;"
					@click="key=item,search()"
					>
						<text>{{item}}</text>
					</view>
				</view>
				<view style="font-size: 15px;;font-weight: 800;margin-left: 2.5vw;display: flex;align-items: center;width:95vw;flex-wrap: wrap;margin-top: 10px;"
				v-if="show2&&searchlist.length>0"
				>
				<view style="display: flex;flex-direction: row;align-items: center;">
					<image src="../../static/time.png" style="width:20px;height:20px;margin-right: 5px;"></image>
					<text>搜索历史</text>
				</view>
				</view>
				<view style="margin-left: 2.5vw;display: flex;align-items: center;width:95vw;flex-wrap: wrap;"
				v-if="show2"
				>
					
					<view v-for="(item,index) in searchlist" style="font-size: 15px;;background-color: #e7ecf3;border-radius: 5px;padding:4px;padding-left:6px;padding-right: 6px;margin-right: 10px;margin-top: 10px;"
					@click="key=item.key,search()"
					>
						<text>{{item.key}}</text>
					</view>
				</view>
				<view style="height:14px;font-size: 14px;color:#909399;;margin-top: 10px;margin-bottom: 10px;display: flex;flex-direction: column;align-items: center;justify-content: center;"
				v-if="searchlist.length>0&&show2"
				>
					<text @click="deletesearch()">清除历史记录</text>
				</view>
				<!---->
				<view style="margin-top:10px;width:100%;margin-left: 5%;font-size: 20px;font-weight: 800;" v-if="userlist.length!=0">
					<text>用户</text>
				</view>
				<!--用户-->
				<view style="width:100%;margin-top: 10px;margin-bottom: 10px;">
					<view v-for="(item,index) in userlist" v-if="index<=5" style="margin-left: 10px;display: flex;flex-direction: column;margin-bottom: 10px;" >
					<view style="display: flex;flex-direction: row;align-items: center;">
						<view style="margin-right: 5px;" @click="heself(item.userid)">
				   		<u-avatar :src="item.userheadimage" v-if="!jugetouxiang(item.userheadimage)"></u-avatar>
				   		<u-avatar randomBgColor :text="item.username.substr(0,1)" v-if="jugetouxiang(item.userheadimage)"></u-avatar>
						</view>
						<view style="margin-left:5px;display: flex;flex-direction: column;height:40px;justify-content: center;">
							<text style="font-size: 16px;">{{item.username}}</text>
					
						</view>
						<view v-if="jugelogin()&&jugemyself(item.userid)" style="margin-left: auto;margin-right: 10px;">
						<view style="width:70px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)" >关注TA</view>
						<view style="width:70px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
						</view>
						</view>
						<view  v-show="index!=userlist.length-1">
							<u-divider style="width:100%;margin: 0 auto;margin-top: 10px;margin-bottom: 10px;"></u-divider>
						</view>
					</view>
					<view  v-if="userlist.length!=0">
						<u-divider text="分割线" :dot="true" style="width:100%;margin: 0 auto;margin-top: 10px;margin-bottom: 10px;"></u-divider>
					</view>
				</view>
				<view style="width:100%;margin-left: 5%;font-size: 20px;font-weight: 800;" v-if="themelist.length!=0">
					<text>主题</text>
				</view>
				<!--主题-->
			<view v-for="(item,index) in themelist" style="width:100vw;;z-index: 0;background-color:white"  v-if="themelist.length!=0" @click="totheme(item.themeid)">
				
				<view  style="width:92%;height:auto;margin-bottom:5px;border-radius: 5px;background-color: white;padding-top:5%;padding-left:4vw;padding-right:4vw;
				padding-bottom:2%
				">
					<view style="width: 100%;padding: 0%;display: flex;flex-direction: row;;
					margin-left: 0%;
					">
						<view style="margin-right: 10px;height:38px;display: flex;
						align-items: center;
						">
								<userhead style="z-index: 1;width:40px;height:40px" :size="'40'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>	
						</view>
						<view style="height:45px;display: flex;flex-direction: column;margin-left: 0px;margin-bottom: 5px;width: 100%;">
							<view>
								<view style="display: flex;flex-direction: row; width:100%;">
									<view style="display: flex;align-items:center">
									<text style="margin-right: 5px;font-size:16px;font-weight: 500;">{{item.username}}</text><text style="font-size: 14px;margin-right:5px" v-if="item.shenfen.length!=0">·</text><u--text :text="item.shenfen" size="13px" color="#909399" :lines="1" v-if="item.shenfen.length!=0"></u--text>
									</view>
									<view style="margin-left: auto;margin-right: 2%;display: flex;flex-direction: row;"> 
										<u-tag text="原创"  plain plainFill size="mini" v-if="item.type==0" type="warning"></u-tag>
										<u-tag text="搬运"  plain plainFill size="mini" v-if="item.type==1" type="warning"></u-tag>
										<u-tag text="精华"  plain plainFill size="mini" v-if="item.jing==1" type="error" style="margin-left: 10px;"></u-tag>
									</view>
								
								</view>
								<view style="display: flex;flex-direction: row;align-items: center;">
									<text style="font-size: 12px;color:#838383;margin-right: 5px;">{{time(item.replytime)}}</text>
									</view>
							</view>
						</view>
					</view>
					<view style="width:100%;margin-left: 0%;margin-right: 0%;display: flex;flex-direction: column;align-items: center;margin-bottom:5px" @click="link(item.themeid)">
						<view style="width:100%">

							<mp-html
							:content="item.title" 
							style="width:100%;font-size: 17px;font-weight: 700;"
							>
								
							</mp-html>
						</view>
						<u--text :lines="5" :text="item.data" size="16" ></u--text>
						
					</view>
					<view  v-if="item.image!=''" style="width:100%;display:flex;;margin-bottom: 10px;margin-top: 10px;">
						<images :image="item.image"></images>
					</view>
					<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
					<u--text @click="link(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
					</view>
					<view v-if="item.tags.length>1" style="display: flex;flex-direction: row;padding-left: 2%;margin-top: 15px;flex-wrap: wrap;">
					<u-tag v-for="(item,index) in item.tags" :text="item"  style="width: auto;margin-right:10px;margin-bottom:5px" size="mini" bgColor="#e1effa" borderColor="#e1effa" color="#5a94ff" @click="linktag(item)"></u-tag>
					</view>
					
					<view style="width:92%;margin-left:4%;display: flex;flex-direction: row;align-items: center;padding-bottom:0px;justify-content: center;padding-top: 0px;
						margin-right:4%;margin-top:15px
					">
						<view style="width:60px;display: flex;flex-direction: row;
						align-items: center;
						
						justify-content: center;" v-show="!jugelike(item.themeid)"
						@click="setlike(item.themeid)"
						>
							<u-icon name="heart"  size="20" style="margin-right: 3px;" color="black"></u-icon>
							<text v-if="item.likes==0" style="font-size:13px;">赞</text>
							<text v-if="item.likes!=0" style="font-size: 13px;">{{item.likes}}</text>
						</view>
						<view style="width:60px;display: flex;flex-direction: row;align-items: center;justify-content: center;" v-show="jugelike(item.themeid)"
						@click="deletelike(item.themeid)"
						>
							<u-icon name="heart-fill" :color="likecolor"  size="20" style="margin-right: 3px;" ></u-icon>
							<text  style="font-size: 13px;">{{item.likes}}</text>
						</view>
						<view style="width:60px;display: flex;justify-content:center;flex-direction: row;align-items: center;;margin-left: 25%;margin-right: 25%;">
							<u-icon  color="black" name="chat"  size="20" style="margin-right: 3px;"></u-icon>
							<text  style="font-size: 13px;">{{item.num}}</text>
						</view>
						<view style="width:60px;display: flex;flex-direction: row;align-items: center;justify-content:center;">
							<u-icon  color="black" name="share"  size="20" style="margin-right: 3px;"></u-icon>
							<text  style="font-size: 13px;">分享</text>
						</view>
					</view>
					
					
				</view>
				<u-gap height="10" bgColor="#f1f2f5"></u-gap>
			</view>
			
			<view>
				<u-loadmore
					    :status="status" 
					    loading-text="努力加载中" 
					    loadmore-text="轻轻上拉" 
					    nomore-text="实在没有了" 
						v-if="show1==1"
						style="margin-top:10px"
						fontSize="12"
						iconSize="14"
				/>
			
				</view>
				
				<!---->
			</view>
		</scroll-view>
			<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	import userhead from '@/pages/index/userhead/userhead.vue'
	import images from "@/pages/index/images/images.vue"
	export default {
		components:{
			userhead,images
		},
		data() {
			return {
				icon:"../../static/icon.png",
				username:"",
				userid:0,
				userheadimage:"",
				userbackgroundimage:"",
				op:1,
				key:"",
				userlist:[],
				status:"",
				getmore:true,
				themelist:[],
				mylike:[],
				attentionlist:[],
				color2:'black',
				searchlist:[],
				show1:0,
				limit:0,
				color1:"white",
				jugetops:[],
				admin:0,
				screenwidth:0,
				screenwidth1:0,
				show2:true,
				hotsearchlist:[],
				likecolor:"#ff007f",
				list:[
					{
											type: 'error',
											icon: false,
											title: '失败主题',
											message: "请登录",
											iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
				],
			}
		},
		onShow(){
			this.userbackgroundimage=getApp().globalData.userbackgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			this.admin=getApp().globalData.admin;
			let _this=this;
			uni.getSystemInfo({
			
			success: function (res){
		_this.screenwidth = res.windowWidth * 0.3
		_this.screenwidth1 =res.windowWidth * 0.9
			}
			
			})
		},
		onLoad(option){
			if(getApp().globalData.skinchoose!=0){
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color2=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=this.color1;
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
			uni.request({
				url:getApp().globalData.http+"/api/hotsearch",
				method:"POST",
				data:{
				},
				success: (res) => {
					if(res.data.code==1001){
						this.hotsearchlist=res.data.data;			
					}
				}
			})
			this.userbackgroundimage=getApp().globalData.userbackgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			this.searchlist=getApp().globalData.searchlist;
			if(option!=null&&option!=undefined)
			this.key=option.key;
			//console.log(this.userheadimage);
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					////console.log("admin:"+getApp().globalData.admin);
					this.op=res.data;
				}
			 });
			this.search();
			this.op=getApp().globalData.op;
			if(getApp().globalData.cookie!='')
			uni.request({
				url:getApp().globalData.http+"/api/jugeuser",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie
				},
				success: (res) => {
					if(res.data.code==1002){
						this.$refs.uToast.show({
							...this.list[0],
							complete() {
								that.loginout();
							}
						})
			
					}
				}
			})
		},
		onBackPress(){
			if(this.themelist.length>0||this.userlist.length>0||this.show1==1){
				this.back();
				return true;
			}
		},
		methods: {
			deletesearch(){
				this.searchlist=[];
				getApp().globalData.searchlist=[];
				uni.setStorage({
					key: "searchlist",
					data: getApp().globalData.searchlist,
					success: function () {
					}
				});
			},
			back:function(){
				
				uni.request({
					url:getApp().globalData.http+"/api/hotsearch",
					method:"POST",
					data:{
					},
					success: (res) => {
						if(res.data.code==1001){
							this.hotsearchlist=res.data.data;			
						}
					}
				})
				if(this.themelist.length>0||this.userlist.length>0||this.show1==1){
					this.themelist=[];
					this.userlist=[];
					this.searchlist=getApp().globalData.searchlist;
					this.show2=true;
					this.show1=0;
					this.key="";
				}else {
					uni.navigateBack();	
				}
			},
			images:function(e){
				return e.slice(";");
			},
			
			search:function(){
				if(this.key==undefined)return;
				this.show2=false;
				this.limit=0;
				var searchsub=0;
				for(var i=0;i<this.searchlist.length;i++){
					if(this.key==this.searchlist[i].key){
						getApp().globalData.searchlist[i].time=new Date().getTime();
						this.searchlist=getApp().globalData.searchlist;
						searchsub=1;
						break;
					}
				}
				if(searchsub==0){
					var temp={
						"key":this.key,
						"time":new Date().getTime()
					}
					getApp().globalData.searchlist.unshift(temp);
					
					if(getApp().globalData.searchlist.length>30)getApp().globalData.searchlist.splice(30,1);
				}
				getApp().globalData.searchlist.sort(function(a,b){
				return a.time<b.time?1:-1;
				});
				this.searchlist=getApp().globalData.searchlist;
				uni.setStorage({
					key: "searchlist",
					data: getApp().globalData.searchlist,
					success: function () {
					}
				});
				uni.request({
					url:getApp().globalData.http+"/api/search",
					method:"POST",
					data:{
						"key":this.key,
						"limit":this.limit,
						"app":1
					},
					success: (res) => {
						for(var i=0;i<res.data.data.theme.length;i++){
					
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/&nbsp;/ig, '');
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/&rdquo;/ig, '');
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/&middot;/ig, '');
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/&mdash;/ig, '');
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/&ldquo;/ig, '');
							res.data.data.theme[i].data = res.data.data.theme[i].data.replace(/\s/ig, '');
							var src=res.data.data.theme[i].image.toString();
							res.data.data.theme[i].image=src.split(";");
							res.data.data.theme[i].image=res.data.data.theme[i].image.slice(0,-1);
							if(res.data.data.theme[i].tags!=undefined){
							res.data.data.theme[i].tags=res.data.data.theme[i].tags.split(";");
							res.data.data.theme[i].tags.pop();
							}
					
						}
						this.themelist=res.data.data.theme;
						this.userlist=res.data.data.user;
						if(this.themelist.length==0&&this.userlist.length==0)
							this.show1=1;
						else this.show1=0;
						this.limit++;
						if(res.data.data.theme.length<10){
							this.getmore=false;
							
						}
				
					}
				})
			},
			getmoretheme:function(){
				if(this.getmore==false)
					return;
				this.getmore=false;
				this.status="loading";
				uni.request({
					url:getApp().globalData.http+"/api/searchmoretheme",
					method:"POST",
					data:{
						"key":this.key,
						"limit":this.limit
					},
					success:(res)=>{
					//	console.log(res.data);
						for(var i=0;i<res.data.data.length;i++){
							res.data.data[i].data = res.data.data[i].data.replace(/&middot;/ig,'');
							res.data.data[i].data = res.data.data[i].data.replace(/&nbsp;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&rdquo;/ig, '');

							res.data.data[i].data = res.data.data[i].data.replace(/&mdash;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&ldquo;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/\s/ig, '');
						
							var src=res.data.data[i].image.toString();
							res.data.data[i].image=src.split(";");
							res.data.data[i].image=res.data.data[i].image.slice(0,-1);
							if(res.data.data[i].tags!=undefined){
							res.data.data[i].tags=res.data.data[i].tags.split(";");
							res.data.data[i].tags.pop();
							}
				
							this.themelist.push(res.data.data[i]);
						}
						this.limit++;
						this.getmore=true;
					if(res.data.data.length<10){
					
						this.getmore=false;
					
						this.status="nomore";
						return;
					}
					}
				})
			},
			test:function(e){
				
				var imgReg = /<img.*?(?:>|\/>)/gi;//定义正则表达式（拿到img标签所有值）
				      
				var deArray  = e.match(imgReg);//使用正则表达式，拿到的是数组
				//["<img src="images/01.gif">", "<img src="images/02.gif">"]
				if (deArray != null && deArray != undefined) {
				        for (var i=0;i<deArray.length;i++) {
				            e = e.replace(deArray[i], "") //放在循环中剔除img标签
				        }
				    }
				
				return e;
				
			},
			time:function(e){
				var g = new Date().getTime()/1000;
				var time=parseInt(g)-parseInt(e);
				if(time<60)
					return "回复于"+parseInt(time)+"秒前";
				else if(time>=60&&time<60*60)
					return "回复于"+parseInt(time/60)+"分钟前";
				else if(time>=60*60&&time<60*60*24)
					return "回复于"+parseInt(time/60/60)+"小时前"
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
					if(year!=year1)
						return year1+"-"+month1+"-"+date1;
					else return month1+"-"+date1;
				}
			},
			jugeattention:function(e){
				this.attentionlist=getApp().globalData.attention;
				for(var i=0;i<this.attentionlist.length;i++){
					if(e==this.attentionlist[i])
						return true;
				}
				return false;
			},
			addattention:function(e){

				uni.request({
					url:getApp().globalData.http+"/api/addattention",
					method:"POST",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"b":e
					},
					success:(res)=>{
						if(res.data.code==1001){
							getApp().globalData.attention.push(e);
							this.attentionlist=getApp().globalData.attention;
						}
					}
				})
			},
			jugemyself:function(e){
				if(e==getApp().globalData.userid)return false;return true;
			},
			deleteattention:function(e){
				uni.request({
					url:getApp().globalData.http+"/api/deleteattention",
					method:"POST",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"b":e
					},
					success:(res)=>{
						if(res.data.code==1001){
							for(var i=0;i<getApp().globalData.attention.length;i++){
								if(getApp().globalData.attention[i]==e){
									getApp().globalData.attention.splice(i,1);
									this.attentionlist=getApp().globalData.attention;
								}
							}
						}
					}
				})
			},
			jugelike:function(res){
				//console.log(this.mylike.length);
				this.mylike=getApp().globalData.mylike;
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
			},
			setlike:function(e){
				if(getApp().globalData.cookie==''){
					this.$refs.uToast.show({
						...this.list[0],
						complete() {
							return;
						}
					})
					return;
				}
				uni.request({
					url:getApp().globalData.http+"/api/setmylike",
					method:"POST",
					data:{
						"themeid":e,
						"userid":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie
					},
					success: (res) => {
						//console.log(res.data.code);
						if(res.data.code==1001){
							this.mylike.push(e);
							for(var i=0;i<this.themelist.length;i++){
								if(this.themelist[i].themeid==e){
									this.themelist[i].likes=this.themelist[i].likes+1;break;
								}
							}
							getApp().globalData.mylike=this.mylike;
							
						}
					}
				})
			},
			linktag:function(e){
				uni.navigateTo({
					url:"./tag?tagname="+e
				})
			},
			jugetouxiang:function(e){
				var touxiang="";
				touxiang=e;
				if(touxiang==undefined){
				return true;
				}
			
				return false;
			},
			heself:function(e){
				uni.navigateTo({
					url:"heself?userid="+e
				})
			},
			deletelike:function(e){
				uni.request({
					url:getApp().globalData.http+"/api/deletemylike",
					method:"POST",
					data:{
						"themeid":e,
						"userid":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie
					},
					success: (res) => {
						if(res.data.code==1001){
							for(var i=0;i<this.mylike.length;i++){
								if(this.mylike[i]==e){
									this.mylike.splice(i,1);
									//console.log(this.mylike);
									getApp().globalData.mylike=this.mylike;
									for(var i=0;i<this.themelist.length;i++){
										if(this.themelist[i].themeid==e){
											this.themelist[i].likes=this.themelist[i].likes-1;break;
										}
									}
									break;
								}
							}
							
						}
					}
				})
			},
			totheme(e){
				uni.navigateTo({
					url:"./theme?themeid="+e
				})
			},
			jugelogin:function(){
				if(getApp().globalData.cookie!='')return true;return false;
			},
			
		}
	}
</script>

<style>

</style>
