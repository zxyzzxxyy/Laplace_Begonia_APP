<template>
	<view style="height:100%;overflow-y: auto;"
	:style="{marginTop:'4.5vh'}"
	>
		<u-list style="height:94.5%;width:100%;background-size: cover;background-attachment: fixed;padding-bottom: 10vh;"  :scroll-y="true" @scrolltolower="getmoretheme">
		<view style="width:100vw;;height:auto;background-color: white;margin: 0 auto;overflow-y: hidden;" 
		>
		
			<view style="margin-bottom: -5vh;z-index: 2;position: absolute;margin-top: 2.5vh;display: flex;flex-direction: row;width: 100vw;align-items: center;">
			
			<view style="margin-left: auto;margin-right: 2.5vw;margin-top: 1vh;">
			<u-icon name="setting-fill" size="25" :color="color1" @click="setting()" ></u-icon>
			</view>
			</view>
			<view style="width:100vw;height:25vh;" >
				<image :src="toutu" style="width:100vw;height:100%" mode="aspectFill" >
					
				<image>
			</view>

			<view style="display: flex;z-index: 1;;flex-direction: row;position: relative;margin-top: -3vh;background-color: white;border-radius: 15px;">
				<view  style="width:170px" v-show="show">
				<view style="z-index: 3;position: absolute;z-index: 2;">
					<userhead :type="1" style="margin-left:20px;margin-top:-50px;width:100px;height:100px" :size="'100'" :username="username" :userheadimage="userheadimage" :headborder="headborder" :pianyi="pianyi"></userhead></view>

				</view>
				<view style="height:auto;margin-top: 0px;display: flex;flex-direction: column;width:80%;justify-content: center;margin-left: 0px;margin-top: 2vh;
				padding-bottom: 0px;"
			
				>
					<view style="z-index: 2;display: flex;flex-direction: row;">
					<view style="margin-left: auto;margin-top: 0px;display: flex;flex-direction: row;width: 100%;justify-content: center;align-items: center;">
						<view style="display: flex;flex-direction: column;align-items: center;"
						@click="tofans()"
						>
							<text>粉丝</text>
							<text style="font-weight: 700;margin-top: 5px;">{{fans}}</text>
						</view>
						<view style="display: flex;flex-direction: column;margin-left: 10%;margin-right: 10%;align-items: center;"
						@click="toattention()"
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
			<view style="width: 95vw;margin-left: 5vw;z-index: 2;position: relative;">
				<text style="font-size: 28px;font-weight: 700;margin-right: auto;">{{username}}</text>
				<view style="margin-top: 10px;">
					<u--text :text="sign" type="info" v-if="sign!=null" ></u--text>
					<u--text text="暂无签名" type="info" v-if="sign==null"></u--text>
				</view>
				<view style="display: flex;flex-direction: row;flex-wrap: warp;margin-top: 10px;">
					<u-tag size="mini" text="添加身份标签" color="#000000" bgColor="#dce0e7" borderColor="#dce0e7" style="margin-right: 0.5rem;" v-if="shenfen.length==0" @click="toshenfen"> </u-tag>
					<view v-for="(item,index) in shenfen" >
						<u-tag size="mini" :text="item.name" plain style="margin-right: 0.5rem;" @click="toshenfen()"> </u-tag>
					</view>
				</view>
			</view>
			<view style="margin-top: 20px;margin-bottom: 10px;">
				<u-gap height="10" bgColor="#f4f4f5" ></u-gap>
			</view>
			<view style="width:95vw;height:50px;border-radius: 15px;background-color: white;margin-bottom: 10px;display: flex;align-items: center;padding-left:2.5vw;padding-right: 2.5vw;
			justify-content: center;
			">
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:#606266" @click="myinfo()">
					<u-icon name="order" color="#606266" size="25"></u-icon><text>我的信息</text>
				</view>
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:#606266" @click="linktomysave()">
					<u-icon name="star" color="#606266" size="25" ></u-icon><text>我的收藏</text>
				</view>
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:#606266" @click="linktomylike()">
					<u-icon name="heart" color="#606266" size="25"></u-icon><text>我的点赞</text>
				</view>
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:#606266" @click="tohistory()">
					<u-icon name="file-text" color="#606266" size="25"></u-icon><text>浏览历史</text>
				</view>
		
				<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:80px;font-size: 14px;color:red" v-if="ban==1" @click="show8=true">
					<u-icon name="warning" color="red" size="25"></u-icon><text>账号停用中</text>
				</view>
			</view>
		</view>
		<view style="margin-top: 0px;margin-bottom: 0px;">
			<u-gap height="10" bgColor="#f4f4f5" ></u-gap>
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
						<text style="font-size: 17px;font-weight: 700;margin-bottom:18px;color:#303133">
							{{item.title}}
						</text>
					</view>
					<u--text  color="#606266" :lines="5" :text="item.data" size="16" ></u--text>
					
				</view>
				<view  v-if="item.image!=''" style="width:100%;display:flex;;margin-bottom: 10px;margin-top: 10px;">
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
		        <view style="width:80vw;height:50vh;padding-top: 20px;padding-left: 10px;padding-right: 10px;;padding-bottom: 10px;overflow-y: auto;border-radius: 10px;">
					<scroll-view style="height: 100%;" scroll-y @scrolltolower="getmoreattention()">
					<view style="width: 100%;display: flex;align-items: center;justify-content: center;margin-bottom: 15px;">
						<text style="font-size: 20px;font-weight: 700;">我的关注</text>
					</view>
		           <view v-for="(item,index) in attentions"  style="margin-left: 5px;display: flex;flex-direction: row;margin-bottom: 20px;height:auto;width:100%">
		           	<view style="margin-right: 5px;" @click="heself(item.userid)">
		           		<u-avatar :src="item.userheadimage" v-if="!jugetouxiang(item.userheadimage)"></u-avatar>
		           		<u-avatar randomBgColor :text="sb(item.username)" v-if="jugetouxiang(item.userheadimage)"></u-avatar>
		           	</view>
		           	<view style="margin-left:5px; display: flex;flex-direction: column;height:40px;justify-content: center;" @click="heself(item.userid)">
		           		<text>{{item.username}}</text>
		           		
		           	</view>
		           	<view style="width:50px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)">关注</view>
		           	<view style="width:50px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
		           </view>
				   <view style="display: flex;flex-direction: column;align-items: center;justify-content: center;margin-bottom: 10px;color:#787878">
				   	<text>没有更多了</text>
				   </view>
					</scroll-view>
		        </view>
		</u-popup>
		<u-popup :show="show2" mode="center"  @close="show2=false" >
		        <view style="width:80vw;height:50vh;padding-top: 20px;padding-left: 10px;padding-right: 10px;;padding-bottom: 10px;overflow-y: auto;border-radius: 10px;">
					<scroll-view style="height: 100%;" scroll-y @scrolltolower="getmorefans()">
					<view style="width: 100%;display: flex;align-items: center;justify-content: center;margin-bottom: 15px;">
						<text style="font-size: 20px;font-weight: 700;">我的粉丝</text>
					</view>
		           <view v-for="(item,index) in fanss"  style="margin-left: 5px;display: flex;flex-direction: row;margin-bottom: 20px;height:auto;width:100%" >
		           	<view style="margin-right: 5px;" @click="heself(item.userid)">
		           		<u-avatar :src="item.userheadimage" v-if="item.userheadimage!=''"></u-avatar>
		           		<u-avatar :text="sb(item.username)" v-if="item.userheadimage==''"></u-avatar>
		           	</view>
		           	<view style="margin-left: 5px;display: flex;flex-direction: column;height:40px;justify-content: center;" @click="heself(item.userid)">
		           		<text>{{item.username}}</text>
		           	
		           	</view>
		           	<view style="width:50px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)">关注</view>
		           	<view style="width:50px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
		           </view>
				   <view style="display: flex;flex-direction: column;align-items: center;justify-content: center;margin-bottom: 10px;color:#787878" >
				   	<text>没有更多了</text>
				   </view>
					</scroll-view>
		        </view>
		</u-popup>
		<!--收藏-->
		<u-popup :show="show8" mode="center"  @close="show8=false">
		        <view style="width:300px;height:auto;padding-top: 20px;padding-left: 10px;padding-right: 10px;;padding-bottom: 20px;overflow-y: auto;border-radius: 10px;color:rgb(120, 120, 120);">
					<text>禁用至:{{time1()}}</text><br>
					<view style="display: flex;flex-direction:row">
						<view>
							<text>禁用原因:</text>
						</view>
						<view>
							<text>{{banreason}}</text>
						</view>
					</view>
				
		        </view>
		</u-popup>
	</view>
</template>

<script>
	import images from "@/pages/index/images/images.vue"
	import MiddleUtil from '@/pages/index/MiddleUtil.js';
	import userhead from '@/pages/index/userhead/userhead.vue'
	export default {
		components:{
			userhead,images
		},
		data() {
			return {
				username:"",
				userheadimage:"",
				userbackgroundimage:"",
				userid:0,
				sign:"",
				color1:"",
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
				headborder:"",
				backvideo:"",
				pianyi:{},
				attention:0,
				themelist:[],
				fanss:[],
				attentions:[],
				attentionlist:[],
				setWidth:0,
				setWidth1:0,
				shenfen:[],
				show:false,
				show1:false,
				show2:false,
				show4:false,
				show5:false,
				show8:false,
				birthday:0,
				banreason:"",
				bantime:0,
				fanspage:0,
				attentionpage:0,
				fansfangdou:0,
				attentionfangdou:0,
				skinchoose:0,
				likecolor:"#ff007f",
			}
		},
		mounted() {
			this.skinchoose=getApp().globalData.skinchoose;
			if(this.skinchoose!=0){
				this.backvideo=getApp().globalData.skin[getApp().globalData.skinchoose-1].backvideo;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
			}
			this.getmyself();
			MiddleUtil.$on('getmyslef',(data)=> {
							this.getmyself();
			})
		},
		methods: {
			myinfo(){
				uni.navigateTo({
					url:"/pages/index/myinfo/myinfo"
				})
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
			tofans(){
				uni.navigateTo({
					url:"/pages/index/myfans"
				})
			},
			toattention(){
				uni.navigateTo({
					url:"/pages/index/myattention"
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
			tohistory(){
				uni.navigateTo({
					url:"/pages/index/history"
				})
			},
			getmoretheme:function(){
				if(this.getmore==false)return;
				this.getmore=false;
				this.status="loading";
				uni.request({
					url:getApp().globalData.http+"/api/getthemelistby_user",
					data:{
						"userid":getApp().globalData.userid,
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
			images:function(e){
				return e.slice(";");
			},
			jugelike:function(res){
				
				this.mylike=getApp().globalData.mylike;
					
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
			},
			heself:function(e){
				uni.navigateTo({
					url:"heself?userid="+e
				})
			},
			head:function(){
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
											this.userheadimage=getApp().globalData.userheadimage;
											uni.setStorage({
											    key: "userheadimage",
											    data: getApp().globalData.userheadimage,
											    success: function () {
											    }
											});			
											this.getmyself();
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
			getmyself(){
				let _this=this;
				uni.getSystemInfo({
				
				success: function (res){
				_this.setWidth1 = res.windowWidth * 0.3
				_this.setWidth =res.windowWidth * 0.9
				}
				
				})
				this.mylike=getApp().globalData.mylike;
				uni.request({
					url:getApp().globalData.http+"/api/getmyattention",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
					
					},
					success: (res) => {
						if(res.data.code==1001){
							getApp().globalData.attention=res.data.data;
							this.attentionlist=getApp().globalData.attention;
						
						}
					}
				})
				if(getApp().globalData.cookie!=''){
				
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
						this.pianyi=res.data.data.pianyi;
						this.headborder=res.data.data.headborder;
						this.bantime=res.data.data.ban_time;
						this.banreason=res.data.data.banreason;
						var i="";
						for(var j=0;j<this.email.indexOf("@")-4;j++)i=i+'x';
							
						this.email=this.email.substring(0,3)+i+this.email.substring(this.email.indexOf("@")-1,this.email.length);
					uni.setNavigationBarTitle({
							title:this.username
						})
					}
				})
				uni.request({
					url:getApp().globalData.http+"/api/getmyfanslist",
					data:{
						"b":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"fanspage":this.fanspage
					},
					method:"POST",
					success: (res) => {
						if(res.data.code==1001){
							this.fanss=res.data.data;
							if(res.data.data.length<15){
								this.fansfangdou=1;
								this.fanspage=-1;
							}else{
								this.fansfangdou=0;
								this.fanspage++;
							}
						}
					}
				})
				this.limit=0;
				uni.request({
					url:getApp().globalData.http+"/api/getthemelistby_user",
					data:{
						"userid":getApp().globalData.userid,
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

				uni.request({
					url:getApp().globalData.http+"/api/getmyattentionlist",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"attentionpage":this.attentionpage
					},
					method:"POST",
					success: (res) => {
						if(res.data.code==1001){
							this.attentions=res.data.data;
							if(res.data.data.length<15){
								this.attentionfangdou=1;
								this.attentionpage=-1;
							}else{
								this.attentionfangdou=0;
								this.attentionpage++;
							}
						}
					}
				})
				
				}
			},
			getmoreattention(){
				if(this.attentionfangdou==1)return this.attentionfangdou=1;
				uni.request({
					url:getApp().globalData.http+"/api/getmyattentionlist",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"attentionpage":this.attentionpage
					},
					method:"POST",
					success: (res) => {
						if(res.data.code==1001){
							for(var i=0;i<res.data.data.length;i++)
								this.attentionlist.push(res.data.data[i]);
							if(res.data.data.length<15){
								this.attentionfangdou=1;
								this.attentionpage=-1;
							}else{
								this.attentionfangdou=0;
								this.attentionpage++;
							}
						}
					}
				})
			},
			getmorefans(){
				if(this.fansfangdou==1)return; this.fangdou=1;
				uni.request({
					url:getApp().globalData.http+"/api/getmyfanslist",
					data:{
						"b":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"fanspage":this.fanspage
					},
					method:"POST",
					success: (res) => {
						if(res.data.code==1001){
							for(var i=0;i<res.data.data.length;i++)
								this.fanss.push(res.data.data[i]);
						if(res.data.data.length<15){
							this.fansfangdou=1;
							this.fanspage=-1;
						}else{
							this.fansfangdou=0;
							this.fanspage++;
						}
						}
					}
				})
			},
			time1(){
				if(this.bantime!=0){
					var now = new Date(this.bantime * 1000); // 依情况进行更改 * 1
						var y = now.getFullYear();
						var m = now.getMonth() + 1;
						var d = now.getDate();
						        return y + "-" + (m < 10 ? "0" + m : m) + "-" + (d < 10 ? "0" + d : d) + " " + now.toTimeString().substr(0, 8);
					
				}
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
			toshenfen:function(){
			//	console.log("xxx");
				uni.navigateTo({
					url:"shenfen"
				})
			},
			linktomylike:function(){
				uni.navigateTo({
					url:"mylike"
				})
			},
			linktomysave:function(){
				uni.navigateTo({
					url:"mysave"
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
		}
	}
</script>

<style>
.videoContainer{
  position: fixed;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -100;
}

.videoContainer:before{
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  display: block;
  z-index: -1;
  top: 0;
  left: 0;
  background: rgba(25,29,34,.65);
  background-size: cover;
}

.fullscreenVideo{
  width: 100%;
  height: 100%;
  object-fit: fill
}
</style>
