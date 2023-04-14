<template>
<view style="padding-top: 4.5vh;background-color: white;height:95.5vh;width:100vw;background-size: cover;background-attachment: fixed;overflow-x: auto;overflow-y: hidden;" v-if="show1">
		<!--顶部栏-->
		<!---->
		<scroll-view  style="width:100%;;height:100vh;border-radius: 0px;overflow-y: auto;;"
	 id="t1" scroll-y     @scrolltolower="getmore()" 			:lowerThreshold="500"
		>
				
				<!--主题-->
				
	<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:100%;"
	>
			<view  style="position: relative;display: flex;flex-direction: column;justify-content: center;width: 100%;height:200px;margin-bottom: 0px;" 
				
			
			>	
				<view style="position: absolute;top:0;margin-top:20px;margin-left: 2vw;width:25px;height:25px;z-index: 6;"  @click="back">
					<u-icon color="white" name="arrow-left" size="25"></u-icon>
				</view>
				<view style="display: flex;flex-direction: row;align-items: center;margin-left:2%;background-color: rgba(255,255,255,0);z-index: 2;margin-top: 30px;">
					<view style="min-width: 25vw;width:25vw;min-width:25vw;height:25vw;border-radius: 10px;overflow: hidden;margin-left: 0px;" v-if="info.imagesrc!=''">
						<image @load="showpage++" style="width:25vw;min-width:25vw;height:25vw" :src="info.imagesrc" mode="aspectFill"></image>
					</view>
					<view style="min-width:25vw;min-height:25vw;width:25vw;height:25vw;border-radius: 10px;;background-color: #909399;color:white;display: flex;align-items: center;justify-content: center;" v-if="info.imagesrc==''">
						<view>
						<text  style="font-size: 30px;">
						{{info.tagname.substr(0,1)}}
						</text>
						</view>
					</view>
					<view style="margin-left: 10px;">
						<view style="font-size: 20px;font-weight: 700;"
						
						>						
							<text  style="font-size: 22px;color:white"
							>
							{{info.tagname}}
							</text>
						</view>
						<view style="display: flex;flex-direction: row;font-size: 15px;margin-top: 3px;margin-bottom: 3px;color:#ffffff" 
					
						>
							<view style="display: flex;flex-direction: row;margin-left: 5px;margin-right: 5px;align-items: center;">
								<u-icon name="eye" size="15" color="#ffffff" style="margin-right: 2px;">
								</u-icon >
								<text>{{info.look}}</text></view>
							<view style="display: flex;flex-direction: row;align-items: center;">
								<u-icon name="chat" size="15" color="#ffffff" style="margin-right: 2px;"></u-icon>
								<text >{{info.num}}</text>
							</view>
						</view>
						<view style="font-size: 15px;" v-if="info.title.length>0">
							<u--text color="white" size="15" :lines="2" :text="'热门 :'+info.title" ></u--text>
						</view>
					</view>
				</view>	
				<view style="width:100%;height:100%;position: absolute;z-index:1;opacity: 0.7;background-color: rgba(0,0,0,0.3);">
					
				</view>
				<view style="width:100%;height:100%;position: absolute;z-index: 0;overflow: hidden;">
					<image :src="info.imagesrc" mode="aspectFill" style="width:100%;filter:blur(8px)"></image>
				</view>
			</view>
			<view style="width:100vw">
				<u-gap height="10" bgColor="#f1f2f5"></u-gap>
			</view>
				<view v-for="(item,index) in themelist "  @click="linkto(item.themeid)"
					style="width:100vw;margin-top: 0vh;margin-bottom: 1vh;background-color: white;border-radius:10px;padding-top:0vh;padding-bottom: 1vh;display:flex;justify-content:center;flex-direction:column"
				>
					<view  style="width:92%;height:auto;margin-bottom:5px;border-radius: 5px;background-color: white;padding-top:5%;padding-left:4vw;padding-right:4vw;
					padding-bottom:2%
					">
						<view style="width: 100%;padding: 0%;display: flex;flex-direction: row;;
						margin-left: 0%;
						">
							<view style="margin-right: 10px;height:38px;display: flex;
							align-items: center;
							">
							<userhead style="z-index: 1;;width:40px;height:40px" :size="'40'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>
								
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
								<text style="font-size: 17px;font-weight: 700;margin-bottom:18px;color:#303133">
									{{item.title}}
								</text>
							</view>
							<u--text :lines="5" :text="item.data" size="16" ></u--text>
							
						</view>
						<view  v-if="item.image!=''" style="width:100%;display:flex;;margin-bottom: 10px;margin-top: 10px;">
							<images :image="item.image"></images>
						</view>
					
					<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
					<u--text @click="link(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
					</view>
						<view style="width:92%;margin-left:4%;display: flex;flex-direction: row;align-items: center;padding-bottom:0px;justify-content: center;padding-top: 0px;
							margin-right:4%;margin-top:15px;
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
				<view style="font-size: 14px;color:#909399;margin-top:-1vh" v-if="page!=-1">
					<text>加载中</text>
				</view>
				<view style="font-size: 14px;color:#909399;margin-top:-1vh" v-if="page==-1">
					<text>没有更多了</text>
				</view>
				</view>
					<view style="height:50px;width:100vw">
						
					</view>
			
		</scroll-view>
		
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
				key:"",
				userid:0,
				userheadimage:"",
				userbackgroundimage:"",
				op:1,
				themelist:[],
				info:{imagesrc:""},
				mylike:[],
				jugetops:[],
				icon:"/static/icon.png",
				admin:0,
				screenwidth:0,
				screenwidth1:0,
				show1:false,
				fangdou:0,
				tagname:"",
				page:0,
				showpage:0,
				rgb:"#ffffff",
				likecolor:"#ff007f",
			}
			
		},
		onShow(){
			this.admin=getApp().globalData.admin;
			let _this=this;
			uni.getSystemInfo({
			
			success: function (res){
			_this.screenwidth = res.windowWidth * 0.3
			_this.screenwidth1 =res.windowWidth * 0.95
			}
			
			})
		},
		onLoad(option){
			this.skinchoose=getApp().globalData.skin;
			uni.setNavigationBarTitle({
				title:option.tagname
			})
			if(this.skinchoose!=0){
				this.likecolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
			}
			let that=this;
			uni.request({
				url:getApp().globalData.http+"/api/gethemelistby_tagname",
				method:"POST",
				data:{
					"tagname":option.tagname,
					"page":0,
					"app":1
				},
				success: (res) => {
					if(res.data.code==1001){
						if(res.data.data.info.imagesrc.length>0){
							uni.request({
								url:res.data.data.info.imagesrc+'?imageAve',
								method:"GET",
								success: (res1) => {
									that.showpage++;
									that.rgb='#'+res1.data.RGB.substr(2,7);
									
								}
							})
						}
						else{
							this.showpage=1;
						}
						for(var i=0;i<res.data.data.themelist.length;i++){
							
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&nbsp;/ig, '');
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&rdquo;/ig, '');
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&middot;/ig, '');
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&mdash;/ig, '');
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&ldquo;/ig, '');
							res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/\s/ig, '');
							
							var src=res.data.data.themelist[i].image.toString();
							res.data.data.themelist[i].image=src.split(";");
							res.data.data.themelist[i].image=res.data.data.themelist[i].image.slice(0,-1);
							if(res.data.data.themelist[i].tags!=undefined){
							res.data.data.themelist[i].tags=res.data.data.themelist[i].tags.split(";");
							res.data.data.themelist[i].tags.pop();
							for(var j=0;j<res.data.data.themelist[i].image.length;j++)
								res.data.data.themelist[i].image[j];
							}
				
						}
						if(res.data.data.themelist.length<5){
							this.fangdou=1;
							this.page=-1;
						}else {this.page++;this.fangdou=0;
						}
						this.themelist=res.data.data.themelist;
						this.info=res.data.data.info;
				
						this.show1=true;
					}
				}
			})
			this.userbackgroundimage=getApp().globalData.userbackgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			
			//console.log(this.userheadimage);
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					////console.log("admin:"+getApp().globalData.admin);
					this.op=res.data;
				}
			 });
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
							...this.upload[2],
							complete() {
								that.loginout();
							}
						})
			
					}
				}
			})
		},
		methods: {
			back:function(){
				uni.navigateBack({
					
				})
			},
			getmore(){
				if(this.fangdou==1)return;this.fangdou=1;
				uni.request({
					url:getApp().globalData.http+"/api/gethemelistby_tagname",
					method:"POST",
					data:{
						"tagname":this.tagname,
						"page":this.page,
						"app":1
					},
					success: (res) => {
						if(res.data.code==1001){
							for(var i=0;i<res.data.data.themelist.length;i++){
								
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&nbsp;/ig, '');
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&rdquo;/ig, '');
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&middot;/ig, '');
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&mdash;/ig, '');
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/&ldquo;/ig, '');
								res.data.data.themelist[i].data = res.data.data.themelist[i].data.replace(/\s/ig, '');
								
								var src=res.data.data.themelist[i].image.toString();
								res.data.data.themelist[i].image=src.split(";");
								res.data.data.themelist[i].image=res.data.data.themelist[i].image.slice(0,-1);
								if(res.data.data.themelist[i].tags!=undefined){
								res.data.data.themelist[i].tags=res.data.data.themelist[i].tags.split(";");
								res.data.data.themelist[i].tags.pop();
								for(var j=0;j<res.data.data.themelist[i].image.length;j++)
									res.data.data.themelist[i].image[j];
								}
												
								this.themelist.push(res.data.data.themelist[i]);
							}
						//	console.log(this.themelist);
							if(res.data.data.themelist.length<5){
								this.page=-1;
								
							}else {this.page++;
							this.fangdou=0;
							}
					
						
						}
					}
				})
			},
			images:function(e){
				return e.slice(";");
			},
			jugetop:function(){
				let that=this;
				var jugetops1=[];
				if(this.themelist.length>0)
				setTimeout(() => {  
					for(var i=0;i<that.themelist.length;i++){
						let info = uni.createSelectorQuery().select("#t"+i);
						info.boundingClientRect(function(data) { //data - 各种参数
						if(data==null)return;
						　　if(data.height>130){
								jugetops1.push(true);
							}
							else jugetops1.push(false);
							that.jugetops=jugetops1;
						}).exec()
						
					}				
					this.$set(this.jugetops,jugetops1);
				},100)
			},
			linkto:function(e){
				uni.navigateTo({
					url:"./theme?themeid="+e
				})
			},
			
			setlike:function(e){
				if(getApp().globalData.cookie==''){
					this.$refs.uToast.show({
						...this.upload[3],
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
			jugelike:function(res){
				//console.log(this.mylike.length);
				this.mylike=getApp().globalData.mylike;
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
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

			link:function(e){
				uni.request({
					url:getApp().globalData.http+"/api/lookadd",
					method:"POST",
					data:{
						"themeid":e
					},
					success: (res) => {
						;
					}
				})
				uni.navigateTo({
					url:"theme?themeid="+e
				})
			},

			linktag:function(e){
				uni.navigateTo({
					url:"tag?tagname="+e
				})
			},

			jugelogin:function(){
				if(getApp().globalData.cookie!='')return true;return false;
			},
			
		}
	}
</script>

<style>
.color1{
	color:black
}
.color2{
	color:white
}
</style>
