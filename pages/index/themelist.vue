<template>
	<view style="height:100vh;">
		<view style="height:100%;position: relative;">
		<u-list style="padding-bottom: 15vh;"
			:preLoadScreen="99999"
			:gundong="!list2"
			@scrolltolower="getthemelistby_fenlei()" 
			@scroll="scroll"
			:scrollTop="scrollTop" 
			:scrollWithAnimation="false"
			:bounce="true"
			:lowerThreshold="500"
			 :throttle="false"
		>	
			<view style="width:100vw">
			<view style="background-size:100vw auto;display: flex;align-items: center;flex-direction: column;width:100vw;position: relative;margin:0 auto;z-index: 3;
"
			:style="{backgroundColor:skincolor,backgroundImage:'url(' + backgroundimage + ')'}"
			>
				<view :style="{backgroundImage:linear1}" style="display: flex;align-items: center;flex-direction: column;width:100vw;position: relative;margin:0 auto;padding-bottom: 0px;">
				<view style="height:4.5vh;width:100vw">
				</view>	
				<view 
				style="transition: 0.05s;width:100vw;display: flex;justify-content: center;flex-direction: row;position: relative;"
				:style="{opacity:topop}"
				>
					<view style="width:10vw;padding-left: 2.5vw;padding-right: 2.5vw;padding-bottom:2vh;;
					transition: 0.05s;;display: flex;flex-direction:row;align-items:center;padding-bottom:2px;justify-content: center;margin-top: 5px;
					"v-if="jugelogin()" 
					
					@click="type=2,getthemelistby_fenlei1({'name':'关注'})">
						<view style="display: flex;flex-direction: column;height:30px" 					:class="{'a44':type==2}">
							<view style=";font-size: 18px;"
							:style="{color:tabcolor1}"
							>关注</view>
						</view>
					</view>

					<view style="width:10vw;padding-right: 2.5vw;padding-left: 2.5vw;;height:padding-bottom:2vh;
					transition: 0.05s;;display: flex;flex-direction:row;align-items:center;padding-bottom:2px;justify-content: center;margin-top: 5px;
					opacity: 1;
					"
					
					:class="{'a3':jugelogin()}"
					@click="type=0,current=0,getthemelistby_fenlei1({'name':'全部分类'})">
						<view style="display: flex;flex-direction: column;height:30px">
							<view :class="{'a44':type==0}" style="font-size: 18px;;"
							:style="{color:tabcolor1}"
							>频道</view>
						</view>
					</view>

					<view style="transition: 0.05s;;position: absolute;height:30px;right:0;margin-right:2.5vw;margin-top: 5px;">
						<u-icon name="search" :color="tabcolor1" size="30"
						@click="search()"
						></u-icon>
					</view>
				</view>
				<view style="z-index: 8;;transition: 0.5s;bottom:0;width:36px;margin-top:-0.5vh
				display: flex;flex-direction: row;justify-content: center;margin-bottom:5px;
				":class="{'l1':type==2&&jugelogin(),'l2':type==0&&jugelogin()}"
					:style="{opacity:topop}"	
					
				>
					<view  style="height:3px;width:20px;margin:0 auto;border-radius: 10px;margin-top:5px"
					:style="{backgroundColor:tabcolor}"
					></view>
				</view>
				</view>
			</view>
			</view>
				<u-sticky   :bgColor="skincolor"  v-if="value==0&&list1.length>0&&type==0" 
				style="margin-bottom:0px;z-index: 2;height:100px;margin-top: -56px;"
				offsetTop="-30"
				>
					<scroll-view style=";flex-direction: row;
					 white-space: nowrap;
					 position: relative;
					height:44px;bottom:5px;position: absolute;"
					
					:style="{backgroundColor:skincolor}"
					:scroll-x="true"
					>
					<u-tabs :list="list1" :current="current"
					@click="getthemelistby_fenlei1" :lineColor="tabcolor"
					@change="changecurrent"
					:activeStyle="{color:tabcolor}"
					:inactiveStyle={color:tabcolor1}
					style="vertical-align:top;display: inline-block;width:93vw;z-index: 1;"
					></u-tabs>
					<view style="display: inline-flex;width:5vw;margin-left:0vw;margin-right:2vw
					background-color: rgba(255,255,255,0);height:44px;
					position:relative;z-index: 3;vertical-align: top;"
			
					class="box"
					>
						<view 
						@click="changelist3"
						style=" 
						background-color: rgba(255,255,255,0);height:100%;
						display: flex;;width:100%;;z-index: 2;align-items: center;justify-content: center;flex-direction: column;">
						<view style="width:100%;height:2px">
						</view>
							<u-icon 
							style=";height:20px;background-color: rgba(255,255,255,0);"  name="list" :color="tabcolor1" size="22"></u-icon>
			
						</view>
						<view
						@click="changelist3"
						 :style="{backgroundImage:linear}"
						 style="width:100%;height:100%;right:5vw;;position:absolute;z-index: 1;">
							
						</view>
					</view>
					</scroll-view>
					<view style=";width:100vw;overflow: hidden;margin-top:100px;"
					:class="{'list1':list2==0,'list2':list2==1}"
					
					>
						<view :style="{Opacity:op1}" style="transition-duration:0.3s;padding-bottom:40px;height:auto;width:100%;background-color:white;display: flex;flex-direction: column;">
							<view style="font-size: 16px;margin-top: 20px;font-weight:700;margin-left: 2%;width:98%">
								<text >全部分区</text>
							</view>
							<view style="transition-duration:0.3s;width:96%;margin-left:2%;display: flex;flex-direction: row;flex-wrap: wrap;">
								<view v-for="(item,index) in list1" 
								@click="changefenlei(item.name,index),loadover=0"
								style="border-radius: 5px;font-size:15px;margin-top:10px;width:30%;margin-left:1%;margin-right:1%;background-color: #f4f4f5;height:35px;display: flex;align-items: center;justify-content: center;">
									<text v-if="current!=index">{{item.name}}</text>
									<text v-if="current==index" style="color:#ff007f">{{item.name}}</text>
								</view>
							</view>
						</view>
						<view :style="{Opacity:op1}" style="transition-duration:0.3s;height:100%;width:100%;background-color:rgba(0, 0, 0, 0.2);"
						@click="changelist3"
						>
							
						</view>
					</view>
				</u-sticky> 
				<view 	v-for="count in 4" v-if="loadover==0">
				<view style="width: 96vw;overflow-x: hidden;border-radius: 3px;padding-top: 5%;"  
			
				>
				
				<u-skeleton
						:loading="true"
					    rows="2"
						:avatar="true"
						:title="false"
						style="margin-left:4vw;"
						avatarSize="40"
						:animate="false"
						:rowsWidth="['200','100']"
						
					/>
					
					<view>
					<view style="width:92vw;margin-left: 4vw;height:20px;border-radius: 5px;
					background-color:#F1F2F4;margin-bottom:10px;margin-top:10px  ;
					">
						
					</view>
					</view>
					
					<view style="width:92vw;margin-left: 4vw;height:100px;border-radius: 5px;
					background-color:#F1F2F4;margin-bottom:20px  ;
					">
						
					</view>
				</view>
				<u-gap height="10" bgColor="#f1f2f5"></u-gap>
				
				</view>
				<view style="display: flex;flex-direction: row;width:100vw;align-items: center;"  v-if="show1&&jugetuijianguanzhu()">
					<view  style="margin-left: 2vw;margin-top: 5px;margin-bottom: 5px;">
						<text style="font-size: 14px;">推荐关注</text>
					</view>
					<view style="margin-top: 5px;;margin-left: auto;margin-right:2vw;"
					 @click="closetuijianguanzhu()"
					>
						<u-icon color="black" name="close" size="12"></u-icon>
					</view>
				</view>
				<scroll-view  v-if="show1&&jugetuijianguanzhu()"  id="a2" scroll-x style=";width:98vw;height:22vh;background-color: white;z-index: 0;;;
				margin-bottom: 0px;padding-top: 0vh;padding-bottom: 0vh;padding-right: 2.5vw;
				">
					<view style="width:auto;height:100%;display:flex;flex-dircetion:row;">
						<view  v-for="(item,index) in fanss" v-if="index<5" style="display: inline-block;width:30rem;border: 1px solid #e6e6e6;height:95%;;margin-left: 10px;margin-right: 10px;border-radius: 10px;padding-left:1rem;padding-right:1rem" >
						<view style="display: flex;width: 25vw;height:90%;padding-top:15%;align-items:  center;flex-direction: column;">
							<view style="" @click="heself(item.userid)">
								<userhead style="z-index: 1;;width:50px;height:50px" :size="'50'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead></view>
							<view style="width:100%;display: flex;justify-content: center;margin-top: 10px;margin-bottom: 10px;flex-direction:column">
								<view style="width:100%;display:flex;justify-content:center;">
								<text style="font-size: 17px;font-weight: 500;">{{item.username}}</text>
								</view>
								<view style="height:24px;width:100%;display:flex;justify-content:center;margin-top:5px;flex-warp:warp;flex-direction:row;margin-bottom:5px">
									<text style="text-align:center;font-size: 12px;color:#909399;">{{item.shenfen1}}</text>
								</view>
							</view>
							<view style="width:100%;height:30px;display: flex;justify-content: center;;margin-bottom:10px">
								<view style="width:90px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;;"  v-show="!jugeattention(item.userid)&&jugemyself(item.userid)" @click="addattention(item.userid)">关注TA</view>
								<view style="width:90px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;"  v-show="jugeattention(item.userid)&&jugemyself(item.userid)" @click="deleteattention(item.userid)">已关注</view>
							</view>
						</view>
							
						</view>
						</view>
				</scroll-view>
				<view v-if="activity.length>0&&type==0" style="border-radius: 10px;overflow: hidden;height:280rpx;width:96vw;margin-left:2vw;margin-top:5px;margin-bottom:0px">
				<Xsuu-swiper :swiperItems="activity"
				style="width:100%"
				:height="280"
				
				:DotPosition="activity.length>1?1:4"
				
				 ></Xsuu-swiper>
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
							<u--text color="#606266" :lines="5" :text="item.data" size="16" ></u--text>
							
						</view>
						<view  v-if="item.image!=''" style="width:100%;display:flex;margin-bottom: 10px;margin-top: 10px;" @click="link(item.themeid)">
						
							<images :image="item.image"></images>
						</view>
						<view v-if="item.position!=undefined&&item.position.length>0" style="margin-left: 0vw;margin-top:0px;margin-bottom:10px;width:55vw">
							<u--text @click="link(item.themeid)" lines="1" prefixIcon="map-fill" :text="item.position" size="14"  color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px;size:17px"></u--text>
						</view>
						<view v-if="item.tags.length>0" style="display: flex;flex-direction: row;padding-left: 2%;margin-top: 10px;flex-wrap: wrap;">
						<u-tag v-if="item1.length>0" v-for="(item1,index) in item.tags" :text="item1"  style="width: auto;margin-right:10px;margin-bottom:5px" size="mini" bgColor="#e1effa" borderColor="#e1effa" color="#5a94ff" @click="linktag(item1)"></u-tag>
						</view>
						
						<view style="width:92%;margin-left:4%;display: flex;flex-direction: row;align-items: center;padding-bottom:0px;justify-content: center;padding-top: 0px;
							margin-right:4%;margin-top:10px;
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
				<!---->
				<view  v-if="themelist.length!=0&&fenlei=='绘画'"
				style="width:95vw;margin-left:2.5vw;margin-top:5%"
				>
					 <custom-waterfalls-flow :value="themelist" imageKey="image" :seat="2" :column="2"   
					 @imageClick="linkto"
					
					 ref="waterfallsFlowRef"
					 >
					 <view class="item" v-for="(item,index) in themelist" :key="index" slot="slot{{index}}"
					 					 
					 >
					                <view class="title">{{item.title}}</view>
					               
					            </view>
					       
					            <template v-slot:default="item" >
					                <view style="width:100%;display: flex;flex-direction:column; background-color:#ffffff ;padding-top:5px;padding-left:0px;padding-bottom: 5px;">
					                 
					                    <u--text :text="item.title" color="#000000" lines="1"></u--text>
										<view style="height:28px;display: flex;flex-direction: row;margin-top: 5px;margin-bottom: 0px;align-items: center;">
											<image :src="item.userheadimage" style="width:28px;height:28px;border-radius: 50%;margin-right:5px;justify-content: center;" mode="aspectFit"></image>
											<u--text :text="item.username" size="14" color="#000000" lines="1"></u--text>
											<view style="margin-left: auto;width:20px;height:20px" v-if="jugelogin()">
												<view style="width:20px;display: flex;flex-direction: row;
												align-items: center;
												
												justify-content: center;" v-show="!jugelike(item.themeid)"
												@click="setlike(item.themeid)"
												>
													
													<u-icon name="heart"  size="20" style="margin-right: 3px;" color="black"></u-icon>
												</view>
												<view style="width:20px;display: flex;flex-direction: row;align-items: center;justify-content: center;" v-show="jugelike(item.themeid)"
												@click="deletelike(item.themeid)"
												>
													
													<u-icon name="heart-fill" :color="likecolor"  size="20" style="margin-right: 3px;" ></u-icon>
												</view>
											</view>
										</view>
					                </view>
					            </template>
					 </custom-waterfalls-flow>
				</view>
				<!---->
				<view style="height:80px;">
					
					<u-loadmore v-if="status=='nomore'&&fenlei!='绘画'"
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
		</view>
	</view>
</template>
<style>
.list1{
	height:0px
}
.list2{
	height:100vh;
	z-index: 10;
}
.l1{
	transform: translateX(-36px);
}
.l2{
	transform: translateX(36px);
}
.a3{
	margin-left: 9px;
}
.a44{
	font-weight: 900;
}
::-webkit-scrollbar {
		    display: none;
		    width: 0 !important;
		    height: 0 !important;
		    -webkit-appearance: none;
		    background: transparent;
		    color: transparent;
		  }
</style>
<script>
	import XsuuSwiper from "@/components/Xss-swiper/Xsuu-swiper.vue"
	import userhead from '@/pages/index/userhead/userhead.vue'
	import images from "@/pages/index/images/images.vue"
	import themes from "@/pages/index/themes/themes.vue"
	export default {
		components:{
			userhead,images,XsuuSwiper,themes
		},
		data() {
			return {
				showtabs:1,
				activity:[],
				loadover:0,
				value:0,
				linear1:"",
				skincolor:'white',
				tabcolor1:"black",
				topop:1,
				op1:0,
				attentionlist:[],
				backgroundimage:"",
				show1:false,
				show2:false,
				list1:[
				],
				list3:[
					
				],
				list2:0,
				linear:'linear-gradient(to left,rgba(255,255,255,1),rgba(255,255,255,0))',
				fanss:[],
				status:"loading",
				keyword:"",
				show:1,
				type:0,
				limit:0,
				scrollTop:0,
				themelist:[],
				leftlist:[],
				mylike:[],
				screenwidth:0,
				fenlei:"全部分类",
				screenwidth1:0,
				h1:0,
				tuijianguanzhu:0,
				h2:0,
				current:0,
				current1:false,
				list2:0,
				tabcolor:"#ff007f",
				searchtuijian:"",
				height:0,
				top:0,
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
				setWidth:0,
				setWidth1:0,
				height1:0,
			}
		},
		mounted(res){
			if(getApp().globalData.skinchoose!=0){
				this.skincolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.tabcolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.tabcolor1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.linear=getApp().globalData.skin[getApp().globalData.skinchoose-1].linear;
				this.linear1=getApp().globalData.skin[getApp().globalData.skinchoose-1].linear1;
				this.backgroundimage=getApp().globalData.skin[getApp().globalData.skinchoose-1].backgroundimage;
				this.likecolor=this.skincolor;
			}
			let that=this;
			uni.getSystemInfo({
				success:function(e){
					that.height=e.windowHeight*0.045;
					that.height1=e.windowHeight*0.045;
				}
			})
	
			this.getthemelist();
			this.tuijian();
		},
		methods: {
			scroll(e){
				var height=this.height;
				if(e<height){
					this.topop=1-e/height;
				}
			},
			jugetuijianguanzhu(){
				this.tuijianguanzhu=getApp().globalData.tuijianguanzhu;
				if(this.tuijianguanzhu==1)return true;return false;
			},
			closetuijianguanzhu(){
				getApp().globalData.tuijianguanzhu=0;
				this.tuijianguanzhu=getApp().globalData.tuijianguanzhu;
			
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
			
			search(){
				uni.navigateTo({
					url:"/pages/index/search"
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
			changefenlei(x,y){
				let temp={
					"name":x,
					"index":y
				}
				this.getthemelistby_fenlei1(temp);
				this.changelist3();
				this.current=y;
			},
			changelist2(){
				this.changelist3();
			},
			jugelogin(){
				if(getApp().globalData.cookie=='')return false;return true;
			},
			changelist3(){
				if(this.op1==0){
					this.list2=1;
					setTimeout(() => {
						this.op1=1;
					}, 10)
				}
				else{
					this.op1=0;
					setTimeout(() => {
						this.list2=0;
					}, 200)
				}
			},
			changecurrent(e){
				this.current=e.index;
				//console.log(argumentsth);
			},
			jugeattention:function(e){
				
				this.attentionlist=getApp().globalData.attention;
			
				for(var i=0;i<this.attentionlist.length;i++){
					if(e==this.attentionlist[i])
						return true;
				}
				return false;
			},
			tuijian(){
				var sub=Math.floor(Math.random() * (20 - 0 + 1)) + 0;
				uni.request({
					url:getApp().globalData.http+"/api/gethottagschart",
					method:"POST",
					data:{},
					success: (res) => {
						{	
							if(res.data.hottagschart[sub].name!=undefined&&res.data.hottagschart[sub].name!=null)
							this.searchtuijian=res.data.hottagschart[sub].name;
						}
												
					}
				})
			},
			newtheme(){
				if(getApp().globalData.cookie==''){
					this.$refs.uToast.show({
					...this.list[0],
					complete() {
						
					}})
					return;
				}
				else{
					uni.navigateTo({
						url:"newtheme"
					})
				}
			},
			text(e){
			
				return e;
			},
			getthemelist(){
				this.loadover=0;
				let _this=this;
				uni.getSystemInfo({
					success: function (res){
					_this.setWidth = res.windowWidth * 0.9;
					_this.setWidth1 = res.windowWidth * 0.30
					}
				
				})
				uni.request({
					url:getApp().globalData.http+"/api/getthemelist",
					data:{
						type:this.type,
						app:1
					},
					method:"POST",
					success: (res) => {
						this.loadover=1;
						
						for(var i=0;i<res.data.data.length;i++){
								var src=res.data.data[i].image.toString();
							res.data.data[i].image=src.split(";");
							res.data.data[i].image=res.data.data[i].image.slice(0,-1);
							if(res.data.data[i].tags!=undefined){
							res.data.data[i].tags=res.data.data[i].tags.split(";");
							res.data.data[i].tags.pop();
							}
						}
						if(res.data.activity.length>0){
							this.activity=[];
					
							for(var i=0;i<res.data.activity.length;i++){
							var temp={
								"img":res.data.activity[i].image.split(";")[0]+'?imageMogr2/thumbnail/1000000@',
								"url":"./theme?themeid="+res.data.activity[i].themeid,
								"title":res.data.activity[i].title,
								"Subtitle":res.data.activity[i].data
							}
							this.activity.push(temp);
							}
						}
						else{
							this.activity=[];
						}
						for(var i=0;i<res.data.data.length;i++){
							res.data.data[i].text='';
							res.data.data[i].data = res.data.data[i].data.replace(/&nbsp;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&rdquo;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&middot;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&mdash;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/&ldquo;/ig, '');
							res.data.data[i].data = res.data.data[i].data.replace(/\s/ig, '');

							
							
							//this.themelist.push(res.data.data[i]);
						}
						this.themelist=res.data.data;
						this.limit++;
					
					}
				})
				uni.request({
					url:getApp().globalData.http+"/api/getfenlei",
					method:"POST",
					data:{
					},
					success: (res) => {
						this.leftlist=[];
						for(var i=0;i<res.data[0].length;i++){
						var temp={
							"title":res.data[0][i],"num":res.data[1][i]
						}
							//console.log(temp);
							this.leftlist.push(temp);
						}
						
						var temp=this.leftlist[this.leftlist.length-1];
						this.leftlist.pop();
						this.leftlist.unshift(temp);
						this.list1=[];
						{
							for(var i=0;i<this.leftlist.length;i++){
								this.list1.push({"name":this.leftlist[i].title,"num":this.leftlist[i].num})
							}
							for(var i=1;i<this.list1.length-1;i++){
								for(var j=i+1;j<this.list1.length;j++){
							
									if(this.list1[i].num<this.list1[j].num){
										var temp=this.list1[j];
										this.list1[j]=this.list1[i];
										this.list1[i]=temp;
									}
								}
							}

						}
					}
				})
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
			login(){
				uni.navigateTo({
					url:"login"
				})
			},
			change4(){
				this.scrollTop=  Math.random();
				this.limit=0;
				if(this.type==2)this.fenlei="关注";
				this.getthemelistby_fenlei1({'name':this.fenlei});
			},
			change5(name) {
				if ((getApp().globalData.cookie=='')&&(name === 3|| name ===2 || name ===4)) return this.login()
				else if(name==2){
					uni.navigateTo({
						url:"/pages/index/newtheme"
					})
				}
				else if(name ===0 ){
				this.value = name	
				}
				else if(name ===1){
				this.value = name	
				this.$refs.find.mounted();
					
				}
				else if(name ===3 ){
				this.value = name	
				}
				else if(name ===4){
				this.value = name
				this.$refs.myself.getmyself();
				}getmyself
				setTimeout(() => { 	
				if(name === 0)
				this.current1=false;
				else{
					this.current1=true;
				}
				}, 100)
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
			getthemelistby_fenlei1:function(e){
				
				this.fenlei=e.name;
				if(this.fenlei=="关注")
					uni.request({
						url:getApp().globalData.http+"/api/userhotlist",
						data:{
							"userid":getApp().globalData.userid
						},
						method:"POST",
						success: (res) => {
							this.show1=true;
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
				else this.show1=false;
				this.select_fenlei=e.index;
				this.getmore=true;
				this.limit=0;
				this.loadover=0;
				this.status="loading";
				let type1=this.type;
				
				if(e.name=="关注"){
					this.fenlei="全部分类";
					type1=2;
				}
				else{
					type1=0;
				}
				{ 
					uni.request({
						url:getApp().globalData.http+"/api/getthemelistby_fenlei",
						method:"POST",
						data:{
							"fenlei":this.fenlei,
							"type":type1,
							"limit":this.limit,
							"userid":getApp().globalData.userid,
							"cookie":getApp().globalData.cookie,
							"app":1
						},
						success: (res) => {
							this.limit++;
							if(res.data.activity.length>0){
							
								this.activity=[];
								for(var i=0;i<res.data.activity.length;i++){
									var temp={
										"img":res.data.activity[i].image.split(";")[0],
										"url":"./theme?themeid="+res.data.activity[i].themeid,
										"title":res.data.activity[i].title,
										"Subtitle":res.data.activity[i].data
								}
								this.activity.push(temp);
								}
							}
							else{
								this.activity=[];
							}
							this.list3=[];
							this.themelist=[];
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
								}
								
								if(this.fenlei=='绘画'){
									if(res.data.data[i].image.length>0){
										this.list3.push({'image':res.data.data[i].image[0]});
									}
								}
								//this.themelist.push(res.data.data[i]);
							}
							this.themelist=res.data.data;	
							setTimeout(() => {
								if(this.fenlei=='绘画')
									this.$refs.waterfallsFlowRef.refresh();
								this.loadover=1;
								this.getmore=true;
								this.scrollTop=  Math.random();
								if(res.data.data.length<10){
									this.getmore=false;
									this.limit=0;
									this.status="nomore";
									return;
								}
							}, 1)
						}
					})
				}
			},
			getthemelistby_fenlei:function(item,index){
				
				if(item!=undefined)this.item=item.title;
				if(index!=undefined)this.index=index;
				if(this.getmore==false)return ;
				this.getmore=false;
				if(getApp().globalData.cookie==''&&this.type==2){
					this.type=0;
				this.$refs.uToast.show({
					...this.upload[3],
					complete() {
						
					}
				})
				}
				this.status="loading";
				{
					uni.request({
						url:getApp().globalData.http+"/api/getthemelistby_fenlei",
						method:"POST",
						data:{
							"fenlei":this.fenlei,
							"type":this.type,
							"limit":this.limit,
							"userid":getApp().globalData.userid,
							"cookie":getApp().globalData.cookie,
							"app":1
						},
						success: (res) => {
							this.limit++;
							this.loadover=1;
							this.list3=[];
							for(var i=0;i<res.data.data.length;i++){
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
					
								if(this.fenlei=='绘画'){
									if(res.data.data[i].image.length>0){
										this.list3.push({'image':res.data.data[i].image[0]});
									}
								}
								this.themelist.push(res.data.data[i]);
							}
							}
							this.getmore=true;
						
							if(res.data.data.length<10){
								this.getmore=false;
								this.limit=0;
								this.status="nomore";
								return;
							}
						}
					})
				}
				}
			},
	}
</script>


