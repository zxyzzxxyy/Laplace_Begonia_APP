<template>
	<view style="height:100%">
		<u-list style="height:100vh;width:100%;background-size: cover;background-attachment: fixed;"  :scroll-y="true" @scrolltolower="getmoretheme">
		<view style="width:100vw;;height:auto;background-color: white;margin: 0 auto;overflow-y: hidden;" 
		>
		
			<view style="margin-bottom: -5vh;z-index: 2;position: absolute;margin-top: 4.5vh;display: flex;flex-direction: row;width: 100vw;align-items: center;">
			
			<view style="display: flex;flex-direction: row;align-items: center;margin-left: 2vw;" >
			<view @click="back">
			<u-icon name="arrow-left"  size="23" style="" ></u-icon>
			</view>
			<view v-if="jugemyself(userid)">
			<u-icon name="email"  size="23" style="margin-left: 80vw;"
			  @click="tochat" 
			 ></u-icon>
			</view>
			</view>
			
			</view>
			<view style="width:100vw;height:25vh">
				<image :src="toutu" style="width:100vw;height:100%" mode="aspectFill" >
					
				<image>
			</view>
			<view style="display: flex;flex-direction: row;position: relative;margin-top: -3vh;background-color: white;border-radius: 15px;">
				<view  style="width:170px" v-show="show">
				<view style="z-index: 3;position: absolute;z-index: 2;">
			<userhead :type="1" style="margin-left:20px;margin-top:-50px;width:100px;height:100px" :size="'100'" :username="username" :userheadimage="userheadimage" :headborder="headborder" :pianyi="pianyi"></userhead></view>	</view>
				
				
				<view style="height:auto;margin-top: 0px;display: flex;flex-direction: column;width:90%;justify-content: center;margin-left: 0px;margin-top: 2vh;
				padding-bottom: 0px;"
			
				>
					
					<view style="z-index: 2;display: flex;flex-direction: row;">
					<view style="margin-left: auto;margin-top: 0px;display: flex;flex-direction: row;width: 100%;justify-content: center;;">
						<view style="display: flex;flex-direction: column;align-items: center;"
						
						>
							<text>粉丝</text>
							<text style="font-weight: 700;margin-top: 5px;">{{fans}}</text>
						</view>
						<view style="display: flex;flex-direction: column;margin-left: 10%;margin-right: 10%;align-items: center;justify-content: center;
						width:48px;
						"
						
						>
							<text>关注</text>
							<text style="font-weight: 700;margin-top: 5px;">{{attention}}</text>
							
						</view>
						<view style="display: flex;flex-direction: column;align-items: center;">
							<text>获赞</text>
							<text style="font-weight: 700;margin-top: 5px;">{{bylike}}</text>
						</view>
						
					</view>
					</view>
					
					
				</view>
			</view>
			<view style="width: 95vw;margin-left: 5vw;margin-top: 10px;">
				<view style="width:100%;display: flex;flex-direction: row;align-items: center;">
					<text style="font-size: 28px;font-weight: 700;margin-right: auto;">{{username}}</text>
					<view style="width:70px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: 10%;margin-right: 5%;"  v-show="!jugeattention(userid)&&jugemyself(userid)" @click="addattention(userid)">关注TA</view>
					<view style="width:70px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: 10%;margin-right: 5%;"  v-show="jugeattention(userid)&&jugemyself(userid)" @click="deleteattention(userid)">已关注</view>
					
				</view>
				<view style="margin-top: 10px;">
					<u--text :text="sign" type="info" v-if="sign!=null" ></u--text>
					<u--text text="暂无签名" type="info" v-if="sign==null"></u--text>
				</view>
				<view style="display: flex;flex-direction: row;flex-wrap: warp;">
						<view v-for="(item,index) in myidentity" style="margin-top: 0.5rem;">	
							<u-tag style="margin-top: 0.5rem;margin-right: 10px;" size="mini" plain="" :text="item.name"
				> </u-tag>
						</view>
						</view>
			</view>
			<view style="margin-top: 20px;margin-bottom: 0px;">
				<u-gap height="10" bgColor="#f4f4f5" ></u-gap>
			</view>
			<view style="width:95vw;height:auto;border-radius: 15px;background-color: white;margin-bottom: 20px;display: flex;align-items: center;padding-left:2.5vw;padding-right: 2.5vw;" v-if="ban==1">
				
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:red" v-if="ban==1">
					<u-icon name="warning" color="red" size="28"></u-icon><text>账号停用中</text>
				</view>
			</view>
		</view>
			<view v-for="(item,index) in themelist" style="width:100vw;;z-index: 0;background-color:white"  v-if="themelist.length!=0">
				
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
					<view style="width:100%;margin-left: 0%;margin-right: 0%;display: flex;flex-direction: column;align-items: center;margin-bottom:5px" @click="linkto(item.themeid)">
						<view style="width:100%">
							<text style="font-size: 17px;font-weight: 700;margin-bottom:18px">
								{{item.title}}
							</text>
						</view>
						<u--text  color="#606266" :lines="5" :text="item.data" size="16" ></u--text>
						
					</view>
					<view  v-if="item.image!=''" style="width:100%;display:flex; ;margin-bottom: 10px;margin-top: 10px;">
						<images :image="item.image"></images>
					</view>
					<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
					<u--text @click="linkto(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
					</view>
					<view v-if="item.tags.length>0" style="display: flex;flex-direction: row;padding-left: 2%;margin-top: 15px;flex-wrap: wrap;">
					<u-tag v-if="item1.length>0" v-for="(item1,index) in item.tags" :text="item1"  style="width: auto;margin-right:10px;margin-bottom:5px" size="mini" bgColor="#e1effa" borderColor="#e1effa" color="#5a94ff" @click="linktag(item1)"></u-tag>
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
						fontSize="12"
						iconSize="14"
						style="margin-top:10px"
				/>
			</view>
		
		</u-list>
		<u-popup :show="show1" mode="center"  @close="show1=false" >
		        <view style="width:80vw;height:auto;padding-top: 20px;padding-left: 10px;padding-right: 10px;;padding-bottom: 10px;overflow-y: auto;border-radius: 10px;">
					<view style="width: 100%;display: flex;align-items: center;justify-content: center;margin-bottom: 15px;">
						<text style="font-size: 20px;font-weight: 700;">TA的关注</text>
					</view>
		           <view v-for="(item,index) in attentions"  style="margin-left: 5px;display: flex;flex-direction: row;margin-bottom: 10px;height:auto;width:100%">
		           	<view style="margin-right: 5px;">
		           		<u-avatar :src="item.userheadimage" v-if="!jugetouxiang(item.userheadimage)"></u-avatar>
		           		<u-avatar randomBgColor :text="sb(item.username)" v-if="jugetouxiang(item.userheadimage)"></u-avatar>
		           	</view>
		           	<view style="display: flex;flex-direction: column;">
		           		<text>{{item.username}}</text>
		           		<view style="display: flex;flex-direction: row;">
		           		<u-tag text="普通会员" size="mini" style="margin-right: 3px;" plain plainFill v-if="item.admin==0"></u-tag>
		           		<u-tag text="管理员" type="error" size="mini" style="margin-right: 3px;" plain plainFill v-if="item.admin==1"></u-tag>
		           		
		           		</view>
		           	</view>
		           	<view style="width:50px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)">关注</view>
		           	<view style="width:50px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
		           </view>
				   <view style="display: flex;flex-direction: column;align-items: center;justify-content: center;margin-bottom: 10px;color:#787878">
				   	<text>没有更多了</text>
				   </view>
		        </view>
		</u-popup>
		<u-popup :show="show2" mode="center"  @close="show2=false" >
		        <view style="width:80vw;height:auto;padding-top: 20px;padding-left: 10px;padding-right: 10px;;padding-bottom: 10px;overflow-y: auto;border-radius: 10px;">
					<view style="width: 100%;display: flex;align-items: center;justify-content: center;margin-bottom: 15px;">
						<text style="font-size: 20px;font-weight: 700;">TA的粉丝</text>
					</view>
		           <view v-for="(item,index) in fanss"  style="margin-left: 5px;display: flex;flex-direction: row;margin-bottom: 10px;height:auto;width:100%" >
		           	<view style="margin-right: 5px;" >
		           		<u-avatar :src="item.userheadimage" v-if="item.userheadimage!=''"></u-avatar>
		           		<u-avatar :text="sb(item.username)" v-if="item.userheadimage==''"></u-avatar>
		           	</view>
		           	<view style="display: flex;flex-direction: column;">
		           		<text>{{item.username}}</text>
		           		<view style="display: flex;flex-direction: row;">
		           		<u-tag text="普通会员" size="mini" style="margin-right: 3px;" plain plainFill v-if="item.admin==0"></u-tag>
		           		<u-tag text="管理员" type="error" size="mini" style="margin-right: 3px;" plain plainFill v-if="item.admin==1"></u-tag>
		           	
		           		</view>
		           	</view>
		           	<view style="width:50px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)">关注</view>
		           	<view style="width:50px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
		           </view>
				   <view style="display: flex;flex-direction: column;align-items: center;justify-content: center;margin-bottom: 10px;color:#787878" >
				   	<text>没有更多了</text>
				   </view>
		        </view>
		</u-popup>
		<!--收藏-->
		
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
				username:"",
				userheadimage:"",
				userbackgroundimage:"",
				pianyi:{},
				headborder:"",
				userid:0,
				sign:"",
				userid1:0,
				toutu:"",
				status:"loading",
				email:"",
				fans:0,
				limit:0,
				ban:0,
				getmore:true,
				registertime:0,
				bylike:0,
				save:0,
				attention:0,
				themelist:[],
				fanss:[],
				attentions:[],
				attentionlist:[],
				setWidth:0,
				setWidth1:0,
				myidentity:[],
				show:true,
				show1:false,
				show2:false,
				show4:false,
				show5:false,
				likecolor:"#ff007f",
			}
		},
		onLoad(user) {
			let _this=this;
			this.skinchoose=getApp().globalData.skinchoose;
			if(this.skinchoose!=0){
				this.likecolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
			}
			uni.getSystemInfo({
				success: function (res){
				_this.setWidth = res.windowWidth * 0.9;
				_this.setWidth1 = res.windowWidth * 0.30
				}
			
			})
			this.attentionlist=getApp().globalData.attention;
			this.userid1=user.userid;
			uni.request({
				url:getApp().globalData.http+"/api/getheself",
				method:"POST",
				data:{
					"userid":parseInt(user.userid)
				},
				success: (res) => {
					this.userid=res.data.data.userid;
					this.username=res.data.data.username;
					this.userheadimage=res.data.data.userheadimage;
					this.userbackgroundimage=res.data.data.userbackgroundimage;
					this.sign=res.data.data.sign;
					this.save=res.data.data.save;
					this.bylike=res.data.data.bylike;
					this.registertime=res.data.data.registertime;
					this.admin=res.data.data.admin;
					this.pianyi=res.data.data.pianyi;
					this.headborder=res.data.data.headborder;
					this.toutu=res.data.data.toutu;
					this.fans=res.data.data.fans;
					this.attention=res.data.data.attention;
					this.myidentity=res.data.shenfen;
				}
			})
			uni.request({
				url:getApp().globalData.http+"/api/getthemelistby_user",
				data:{
					"userid":parseInt(user.userid),
					"limit":this.limit,
					"app":1,
				},
				method:"POST",
				success: (res) => {
					for(var i=0;i<res.data.data.length;i++){
						res.data.data[i].text='';
						res.data.data[i].data = res.data.data[i].data.replace(/&nbsp;/ig, '');
						res.data.data[i].data = res.data.data[i].data.replace(/&rdquo;/ig, '');
						res.data.data[i].data = res.data.data[i].data.replace(/&middot;/ig, '');
						res.data.data[i].data = res.data.data[i].data.replace(/&mdash;/ig, '');
						res.data.data[i].data = res.data.data[i].data.replace(/&ldquo;/ig, '');
						res.data.data[i].data = res.data.data[i].data.replace(/\s/ig, '');
						var src=res.data.data[i].image.toString();
						res.data.data[i].image=src.split(";");
						res.data.data[i].image=res.data.data[i].image.slice(0,-1);
						if(res.data.data[i].tags!=undefined){
						res.data.data[i].tags=res.data.data[i].tags.split(";");
						res.data.data[i].tags.pop();
						for(var j=0;j<res.data.data[i].image.length;j++)
							res.data.data[i].image[j]+="?imageMogr2/format/webp";
						}
					
					}
			
					this.limit++;
					this.themelist=res.data.data;
					if(res.data.data.length<10){
						this.getmore=false;
						this.status="nomore";
					}
				}
			})
		},
		methods: {
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
			images:function(e){
				return e.slice(";");
			},
			jugelike:function(res){
				
				this.mylike=getApp().globalData.mylike;
					
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
			},
			tochat:function(){
				var url="chat?userid="+this.userid+"&username="+this.username+"&userheadimage="+this.userheadimage;
				uni.navigateTo({
					url:url
				})
			},
			jugeattention:function(e){
				this.attentionlist=getApp().globalData.attention;
				for(var i=0;i<this.attentionlist.length;i++){
					if(e==this.attentionlist[i])
						return true;
				}
				return false;
			},
			linktag:function(e){
				uni.navigateTo({
					url:"tag?tagname="+e
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
			sb(e){
				var str='';str+=e;
				return str.substr(0,1);
			},
			getmoretheme:function(){
				if(this.getmore==false)return;
				this.getmore=false;
				this.status="loading";
				uni.request({
					url:getApp().globalData.http+"/api/getthemelistby_user",
					data:{
						"userid":parseInt(this.userid),
						"limit":this.limit,
						"app":1
					},
					method:"POST",
					success: (res) => {
						for(var i=0;i<res.data.data.length;i++){
							res.data.data[i].text='';
							res.data.data[i].data = res.data.data[i].data.replace(/&nbsp;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&rdquo;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&middot;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&mdash;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&ldquo;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/\s/ig, '');
							var src=res.data.data[i].image.toString();
							res.data.data[i].image=src.split(";");
							res.data.data[i].image=res.data.data[i].image.slice(0,-1);
							if(res.data.data[i].tags!=undefined){
							res.data.data[i].tags=res.data.data[i].tags.split(";");
							res.data.data[i].tags.pop();
							for(var j=0;j<res.data.data[i].image.length;j++)
								res.data.data[i].image[j]+="?imageMogr2/format/webp";
							}
						
							this.themelist.push(res.data.data[i]);
						}
						this.limit++;
						
						this.getmore=true;
						if(res.data.data.length<10){
							this.getmore=false;
							this.status="nomore";
						}
					
					}
				})
			},
			
			linkto(e){
				uni.navigateTo({
					url:"./theme?themeid="+e
				})
			},
			setting(){
				uni.navigateTo({
					url:"setting"
				})
			},
			back(){
				uni.navigateBack({
					delta:1
				})
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
			time2:function(e){
				var d = new Date(e*1000);
				var year = d.getFullYear();
				var month = d.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
				var date = d.getDate(); 
				return year+"-"+month+"-"+date;
			},
			jugemyself:function(e){
				if(e==getApp().globalData.userid)return false;return true;
			},
			jugeattention:function(e){
				
				this.attentionlist=getApp().globalData.attention;
			
				for(var i=0;i<this.attentionlist.length;i++){
					if(e==this.attentionlist[i])
						return true;
				}
				return false;
			},
		}
	}
</script>

<style>

</style>
