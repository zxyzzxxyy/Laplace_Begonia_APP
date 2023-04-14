<template>
	<view>
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
				 style="font-weight: 700;">我的点赞</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:0px">
			1
		</view>
		<scroll-view style="height:100vh" scroll-y @scrolltolower="getmore()">
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
					<u--text  color="#606266" :lines="5" :text="item.data" size="16" ></u--text>
					
				</view>
				<view  v-if="item.image!=''" style="width:100%;display:flex;margin-bottom: 10px;margin-top: 10px;">
					<images :image="item.image"></images>
				</view>
				<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
				<u--text @click="link(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
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
		
		<view style="padding-bottom: 0px;">
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
				themelist:[],
				page:0,
				fangdou:0,
				status:"loading",
				setWidth1:0,
				setWidth:0,
				color:"white",
				color1:"black",
				likecolor:"#ff007f",
			}
		},
		onLoad(){
			if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
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
			let _this=this;
			uni.getSystemInfo({
			
			success: function (res){
			_this.setWidth = res.windowWidth * 0.3
			_this.setWidth1 =res.windowWidth * 0.9
			}
			
			})
			uni.request({
				url:getApp().globalData.http+"/api/getmylike",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie,
					"userid":getApp().globalData.userid
				},
				success: (res) => {
					if(res.data.code==1001){
						getApp().globalData.mylike=res.data.mylike
					}
				}
			})
			uni.request({
				url:getApp().globalData.http+"/api/getmylikelist",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie,
					"userid":getApp().globalData.userid,
					"likepage":this.page
				},
				success: (res) => {
					if(res.data.code==1001){
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
						this.themelist=res.data.data;
						if(res.data.data.length<5){
							this.status="nomore";
							this.fangdou=1;
						}else{
							this.fangdou=0;
							this.page++;
						}
					}
				}
			})
		},
		methods: {
			back(){
				uni.navigateBack();
			},
			getmore(){
				if(this.fangdou==1)return this.fangdou=1;
				uni.request({
					url:getApp().globalData.http+"/api/getmylikelist",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"likepage":this.page
					},
					success: (res) => {
						if(res.data.code==1001){
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
							
						
							if(res.data.data.length<5){
								this.status="nomore";
								this.fangdou=1;
							}else{
								this.fangdou=0;
								this.page++;
							}
						}
					}
				})
			},
			linktag:function(e){
				uni.navigateTo({
					url:"/pages/index/tag?tagname="+e
				})
			},
			link:function(e){
				uni.navigateTo({
					url:"./theme?themeid="+e
				})
			},
			
		
			jugelike:function(res){
				//console.log(this.mylike.length);
				this.mylike=getApp().globalData.mylike
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
		
			images:function(e){
				return e.slice(";");
			},
		}
	}
</script>

<style>

</style>
