<template>
<view style="background-color: white;height:100vh;width:100vw;background-size: cover;background-attachment: fixed;overflow-x: auto;overflow-y: hidden;" >
		<!--顶部栏-->
		
		<!--主题-->
		<u-sticky >
		<view  style="background-size:100vw auto;width:95vw;padding-left: 2.5vw;padding-right: 2.5vw;padding-top: 5vh;padding-bottom: 0.75vh;		
		" :style="{backgroundColor:skincolor,backgroundImage:'url(' + backgroundimage + ')'}">
		<u-search  :placeholder="searchtuijian" v-model="keyword" @search="search" :showAction="false"></u-search>
		</view>
		</u-sticky>
		<view style="width:100%;display: flex;justify-content: center;height:110vh;overflow-y: hidden" >
		
		<scroll-view scroll-y="false" style="width:100%;height:auto;padding-bottom: 10%;padding-top:8px;padding-bottom: 17vh;overflow-y: auto;"
		:scroll-into-view="tag" :loadmoreoffset="15" :scroll-with-animation="false"   :scroll-top="top"
		@scrolltolower="getmorehot()" :lower-threshold="500"
		>

		<view id="a3">
			<view  style="width:96vw;height:300rpx;background-color: white;margin-left: 2vw;
			display: flex;justify-content: center;;overflow: hidden;border-radius: 5px;
			">
				<view >
				
				<Xsuu-swiper :swiperItems="swiperItems"
				style="width:96vw;"
				:height="300"
				v-if="loadok"
				 ></Xsuu-swiper>
				 
				 <u-skeleton
				 	    rows="1"
				 		rowsHeight="300rpx"
				 		rowWidth="95%"
				 		:title="false"
				 						v-if="!loadok"
				 	/>
				 </view>

			</view>
		</view>

		<scroll-view scroll-x style="width:96vw;margin-right: 2vw;;margin-left:2vw;height:27.5vw;">
			<view style="display:flex;flex-direction: row;margin-bottom: 10px;height:27.5vw;width: auto;">
			<view style="min-width:22.5vw;height:22.5vw;border-radius: 10px;margin-right:2vw;margin-top:10px;position: relative;"
			 v-for="(item,index) in taglist1 "
			@click="linktag(item.title)"
			
		
			>
				<image mode="aspectFill"  style="width:22.5vw;height:22.5vw;border-radius: 5px;position: absolute;" :src="item.img">

				</image>
				<view style="width:18.5vw;height:18.5vw;border-radius:5px;padding:2vw;background-color:rgba(0, 0, 0, 0.3);position: absolute;">
					<u--text :text="item.title" color="white" size="15" lines="2"></u--text>
					<u--text prefixIcon="eye" iconStyle="font-size: 15px;color:white" color="white" size="13" style="bottom:0px;position: absolute;margin-bottom:3px" :text="item.num"></u--text>
				</view>
			</view>
			</view>
		</scroll-view>
		
				<u-gap height="10" bgColor="#f1f2f5"></u-gap>

			<view id="a1" style="padding-top:0px">
			<view v-for="(item,index) in themelist" style="width: 100%;;" >
			<view  style="width:92%;height:auto;margin-bottom:5px;border-radius: 5px;background-color: white;padding-top:5%;padding-left:4vw;padding-right:4vw;
			padding-bottom:2%
			">
				<view style="width: 100%;padding: 0%;display: flex;flex-direction: row;;
				margin-left: 0%;
				">
					<view style="margin-right: 10px;height:38px;display: flex;
					align-items: center;z-index:0
					">
						<userhead style="width:40px;height:40px" :size="'40'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>	
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
				<view  v-if="item.image!=''" style="width:100%;display:flex;;margin-bottom: 10px;margin-top: 10px;">
					<images :image="item.image"></images>
				</view>
				<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
				<u--text @click="link(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
				</view>
				<view v-if="item.tags.length>0" style="display: flex;flex-direction: row;padding-left: 2%;margin-top: 10px;flex-wrap: wrap;">
				<u-tag v-if="item1.length>0" v-for="(item1,index) in item.tags" :text="item1"  style="width: auto;margin-right:10px;margin-bottom:5px" size="mini" bgColor="#e1effa" borderColor="#e1effa" color="#5a94ff" @click="linktag(item1)"></u-tag>
				</view>
				<view style="width:92%;margin-left:4%;display: flex;flex-direction: row;align-items: center;padding-bottom:0px;justify-content: center;padding-top: 0px;
					margin-right:4%;margin-top:10px
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
			
			</view>
			<view style="height:80px;">
				
				<u-loadmore v-if="status=='nomore'"
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
		<view>
				<u-toast ref="uToast"></u-toast>
				
		</view>
	</view>
</template>

<script>
	import XsuuSwiper from "@/components/Xss-swiper/Xsuu-swiper.vue"
	import userhead from "@/pages/index/userhead/userhead.vue"
	import images from "@/pages/index/images/images.vue"
	export default {
		components: {XsuuSwiper,userhead,images},
		data() {
			return {
				a1:0,
				a2:0,
				a3:0,
				arr:['50%'
				],
				choose:0,
				tag:"",
				userbackgroundimage:"",
				username:"",
				userheadimage:"",
				chartData2:{
					series:[
						
					]
				},
				themelist:[],
				attentionlist:[],
				setWidth:0,
				setWidth1:0,
				taglist1:[],
				op:1,
				type:0,
				admin:0,
				limit:0,
				likecolor:"#ff007f",
				mylike:[],
				taglist:[],
				fanss:[],
				loadok:false,
				status:"loadmore",
				skincolor:"white",
				searchtuijian:"",
				keyword:"",
				loadok1:false,
				icon:"/static/icon.png",
				top:0,
				fangdou:1,
				linear:"",
				linear1:"",
				backgroundimage:"",
				show1:false,
				swiperItems:[
			                    /*{
			                            "img": "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fn.sinaimg.cn%2Fsinacn11%2F440%2Fw744h496%2F20181030%2F97c2-hnaivxq7344712.jpg&refer=http%3A%2F%2Fn.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1619914829&t=52a970d21d4898c8e7ca21b8b5aa9312",
			                            "title": "鲤程新能源",
			                            "Subtitle": "心鲤程，心鲤想！",
			                            "tip": "限时",
			                            "url": "111"
			                        },*/
				],
				list:[
					{
						type: 'error',
						title: "失败",
						message:"请登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
				]
			}
		},
		mounted: function () { 
			if(getApp().globalData.skinchoose!=0){
				this.skincolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.linear=getApp().globalData.skin[getApp().globalData.skinchoose-1].linear;
				this.linear1=getApp().globalData.skin[getApp().globalData.skinchoose-1].linear1;
				this.backgroundimage=getApp().globalData.skin[getApp().globalData.skinchoose-1].backgroundimage;
				this.likecolor=this.skincolor;
			}
		this.load();
		},
		
		methods: {

			backtop(){
				this.top=Math.random();
				this.load();
			},
			getmorehot(){
				if(this.limit==-1||this.fangdou==1)return;
				this.fangdou=1;
				this.status="loading";
				uni.request({
					
					url:getApp().globalData.http+"/api/getthemelistby_hot",
					data:{
						app:1,
						limit:this.limit
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
							this.themelist.push(res.data.data[i]);
						}
					}
					if(res.data.data.length<10){
						this.limit=-1;
						this.status="nomore";
					}
					else {
					
						this.limit++;
						this.status="loadmore";
					}
					this.fangdou=0;
					}
				})
			},
			load(){
				var sub=Math.floor(Math.random() * (20 - 0 + 1)) + 0;
				uni.request({
					url:getApp().globalData.http+"/api/gethottagschart",
					method:"POST",
					data:{},
					success: (res) => {
						{	
							this.searchtuijian=res.data.hottagschart[sub].name;
						}
												
					}
				})
				let _this=this;
				uni.getSystemInfo({
					success: function (res){
					_this.setWidth = res.windowWidth * 0.95;
					_this.setWidth1 = res.windowWidth * 0.30
					}
				
				})
					this.admin=getApp().globalData.admin;
					this.attentionlist=getApp().globalData.attentionlist;
					this.mylike=getApp().globalData.mylike;
				
					this.op=getApp().globalData.op;
					this.username=getApp().globalData.username;
					this.userheadimage=getApp().globalData.userheadimage;
					this.userbackgroundimage=getApp().globalData.userbackgroundimage;
					var id=0;
					if(getApp().globalData.userid!='')id=getApp().globalData.userid;
					uni.request({
						url:getApp().globalData.http+"/api/userhotlist",
						data:{
							"userid":id
						},
						method:"POST",
						success: (res) => {
							
							for(var i=0;i<res.data.length;i++){
				
								if(res.data[i].userid!=getApp().globalData.userid){
									if(res.data[i]?.shenfen&&res.data[i].shenfen.length>0){
										var str="";
										for(var j=0;j<res.data[i].shenfen.length-1;j++){
											str+=res.data[i].shenfen[j].name+='、';
										}
										str+=res.data[i].shenfen[res.data[i].shenfen.length-1].name;
										res.data[i].shenfen1=str;
										
									}
									//this.fanss.push(res.data[i]);
								}
								this.fanss=res.data;
							}
							this.loadok1=true;
						}
					})
					uni.request({
						url:getApp().globalData.http+"/api/gethottagschart",
						method:"POST",
						data:{},
						success: (res) => {
							
							{
								var temp=[];
								for(var i=0,j=30;i<res.data.hottagschart.length;i++,j--){
									temp.push({
										"name":res.data.hottagschart[i].name,
										"textSize":j,
										"data":undefined
									})
								}
								this.chartData2.series=temp;				
							}
													
						}
					})
					uni.request({
						url:getApp().globalData.http+"/api/gethottag",
						data:{
						},
						method:"POST",
						success: (res) => {
							if(res.data.code==1001){
								this.swiperItems=[];
								this.taglist1=[];
								this.taglist=res.data.data;
								var temp1=[];
								for(var i=0;i<res.data.data.length;i++){
									var temp={
										"img":res.data.data[i].imagesrc+'?imageMogr2/thumbnail/1000000@',
										"title":res.data.data[i].tagname,
										"Subtitle":res.data.data[i].title,
										"num":res.data.data[i].look,
										"url":"./tag?tagname="+res.data.data[i].tagname
									}
									this.loadok=true;
									if(i<3)
									this.swiperItems.push(temp);
									if(i>2){
										if(res.data.data[i].imagesrc.length>0)
										this.taglist1.push(temp);
										else temp1.push(temp);
									}
								}
								for(var j=0;j<temp1.length;j++)this.taglist1.push(temp1[j]);
							
							}
						}
					})
					if(getApp().globalData.cookie!='')
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
					
							}
						}
					})
					uni.request({
						
						url:getApp().globalData.http+"/api/getthemelistby_hot",
						data:{
							app:1
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
							this.themelist=res.data.data;
							this.show1=true;
							if(res.data.data.length<10){
								this.limit=-1;
								this.status="nomore";
							}
							else {
								this.limit=this.limit+1;
							this.status="loadmore";
							}
							this.fangdou=0;
						}
					})
			},
			search:function(value){
				if(value=="")
				uni.navigateTo({
					url:"search?key="+this.searchtuijian
				})
				else
				uni.navigateTo({
					url:"search?key="+value
				})
			},
			linktag1:function(e){
				//console.log(this.chartData2);
				uni.navigateTo({
					url:"tag?tagname="+this.chartData2.series[e.currentIndex].name
				})
			},
			images:function(e){
				return e.slice(";");
			},
			linktag:function(e){
				uni.navigateTo({
					url:"tag?tagname="+e
				})
			},
			heself:function(e){
				if(e==getApp().globalData.userid)return;
				uni.navigateTo({
					url:"heself?userid="+e
				})
			},
			addattention:function(e){
				if(getApp().globalData.cookie==""){
					this.$refs.uToast.show({
						...this.list[0],
						complete() {
						}
					})
				}
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
			changetag:function(e){
				if(e=="a1")this.tag="a1"; else if(e=="a2")this.tag="a2";else this.tag="a3";return;
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
			jugelike:function(res){
				this.mylike=getApp().globalData.mylike;
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
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
					url:"./theme?themeid="+e
				})
			},
			
			
		
		}
	}
</script>

<style>

</style>
