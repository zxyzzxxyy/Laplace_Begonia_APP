<template>
	<view>
		<view  v-if="themelist.length!=0&&fenlei=='绘画'"
		style="width:95vw;margin-left:2.5vw;margin-top:5%"
		>
			 <custom-waterfalls-flow :value="themelist" imageKey="image" :seat="2" :column="2"   
			 @imageClick="linkto"
			 @wapperClick="linkto"
			 ref="waterfallsFlowRef"
			 >
			 <view class="item" v-for="(item,index) in themelist" :key="index" slot="slot{{index}}"
				v-if="item.image.length>0"
			 >
							<view class="title">{{item.title}}</view>
						   
						</view>
				   
						<template v-slot:default="item" >
							<view style="width:100%;display: flex;flex-direction:column; background-color:#ffffff ;padding-top:5px;padding-left:0px;padding-bottom: 5px;">
							 
								<u--text :text="item.title" color="#000000" lines="1"></u--text>
								<view style="height:28px;display: flex;flex-direction: row;margin-top: 5px;margin-bottom: 0px;">
									<image :src="item.userheadimage" style="width:28px;height:28px;border-radius: 50%;margin-right:5px;justify-content: center;" mode="aspectFit"></image>
									<u--text :text="item.username" size="14" color="#000000" lines="1"></u--text>
								</view>
							</view>
						</template>
			 </custom-waterfalls-flow>
		</view>
		<view  style="z-index: 1;" v-for="(item,index) in themelist"  v-if="themelist.length!=0&&fenlei!='绘画'">
			
			<view  style="width:92%;height:auto;margin-bottom:5px;border-radius: 5px;background-color: white;padding-top:5%;padding-left:4vw;padding-right:4vw;
			padding-bottom:2%
			">
				<view style="width: 100%;padding: 0%;display: flex;flex-direction: row;;
				margin-left: 0%;
				">
					<view style="margin-right: 10px;height:38px;display: flex;
					align-items: center;position: relative;
					"><!--
					<u-avatar mode="aspectFill":src="item.userheadimage" v-if="item.userheadimage!=null" size="38"></u-avatar>
					<u-avatar :text="item.username.substr(0,1)"  randomBgColor v-if="item.userheadimage==null" size="38"></u-avatar>-->
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
					<u--text color="#606266" :lines="5" :text="item.data" size="16" ></u--text>
					
				</view>
				<view  v-if="item.image!=''" style="width:100%;display:flex;margin-bottom: 10px;margin-top: 10px;" @click="link(item.themeid)"
					<images :image="item.image"></images>
				</view>
				<view v-if="item.tags.length>0" style="display: flex;flex-direction: row;padding-left: 2%;margin-top: 15px;flex-wrap: wrap;">
				<u-tag v-if="item1.length>0" v-for="(item1,index) in item.tags" :text="item1"  style="width: auto;margin-right:10px;margin-bottom:5px" size="mini" bgColor="#e1effa" borderColor="#e1effa" color="#5a94ff" @click="linktag(item1)"></u-tag>
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
						<u-icon name="heart-fill" color="#ff007f"  size="20" style="margin-right: 3px;" ></u-icon>
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
					<view style="padding-top: 15px;;">
					<u-gap height="10" bgColor="#f1f2f5"></u-gap>
					</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	import XsuuSwiper from "@/components/Xss-swiper/Xsuu-swiper.vue"
	import userhead from '@/pages/index/userhead/userhead.vue'
	import images from "@/pages/index/images/images.vue"
	export default {
		components:{
			userhead,images,XsuuSwiper
		},
		data() {
			return {
				attentionlist:[],
				mylike:[],
			}
		},
		props:{
			themelist:{
				type:Array,
				default:()=>[""],
				require:true
			},
			fenlei:{
				type:String,
				default:"",
				require:false
			}
		},
		watch:{
				fenlei: {
				    handler(newVal, oldVal) {
				        this.$refs.waterfallsFlowRef.refresh();
				    },
					immediate: true
			}
		},
		mounted: () => {
		
			if(getApp().globalData.cookie!=''){
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
							this.mylike=res.data.mylike;
							
						}
					}
				})
			}
		},
		methods: {
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
			jugemyself:function(e){
				if(e==getApp().globalData.userid)return false;return true;
			},
			linkto(e){
				uni.navigateTo({
					url:"/pages/index/theme?themeid="+e.themeid
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
			heself:function(e){
			
					
				uni.navigateTo({
					url:"heself?userid="+e
				})
			},
			setlike:function(e){
				if(getApp().globalData.cookie==''){
					uni.navigateTo({
						url:"/pages/index/login"
					})
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
			jugelike:function(res){
				
				this.mylike=getApp().globalData.mylike;
					
				for(var i=0;i<this.mylike.length;i++)
					if(this.mylike[i]==res)return true;return false
			},
			linktag:function(e){
				uni.navigateTo({
					url:"./tag?tagname="+e
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
		}
	}
</script>

<style>

</style>
