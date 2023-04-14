<template>
	<view style="height:100vh;overflow-y: auto;">
		<view style="width:100vw;height:110px;border-bottom:solid 0.5px #b3b7be;position: absolute;display:flex;flex-direction:column;align-items:center;justify-content: center;;transform: 0.2s;transition: 0.2s" :style="{backgroundColor:skincolor
		}"
		:class="{'op1':show9==1,'op0':show9==0,'op2':show9==2}"
		
		>	
			<view style="width:100vw;display: flex;align-items:center;justify-content: center;;
			
			">
			<userhead headborder="" :pianyi="{}" :type="1" style="width:30px;height:30px;margin-top: 33px;margin-bottom:2px; " :size="'30'" :username="username" :userheadimage="userheadimage"
			 
			 ></userhead>
			 </view>
			 <view style="border-radius:15px 15px 0 0;width:100vw;margin-top: 5px;padding-bottom:5px;height:40px;background-color: white;display: flex;flex-direction: column;align-items:center;justify-content: center;border-bottom: 0.5px solid #cdd2da;">
				 <view style="width:50vw;display: flex;flex-direction: row;align-items: center;justify-content: center;">
				 	<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;">
				 		<text style="" v-if="selectpage==0">主题</text>
				 		<text style="color:#909399" v-if="selectpage!=0"
				 		@click="selectpage=0"
				 		>主题</text>
				 
				 	</view>
				 	<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;margin-left:30px;margin-right:30px">
				 		<text style=""v-if="selectpage==1">点赞</text>
				 		<text style="color:#909399"v-if="selectpage!=1"
				 		@click="selectpage=1"
				 		>点赞</text>
				 	</view>
				 	<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;">
				 		<text style=""v-if="selectpage==2">收藏</text>
				 		<text style="color:#909399"v-if="selectpage!=2"
				 		@click="selectpage=2"
				 		>收藏</text>
				 	</view>
				 </view>
				 
				 <view style="100vw;display: flex;align-items: center;">
				 	<view style="width:50vw;display: flex;justify-content: center;">
				 	<view style="width:28px;height:2px;border-radius: 5px;margin-top: 5px;transition: 0.2s;"
				 	:style="{backgroundColor:skincolor}"
				 	:class="{'left1':selectpage==0,'left2':selectpage==2}"
				 	>
				 		
				 	</view>
				 	</view>
				 </view>
			 </view>
		</view>
		<u-list @scroll="scroll" style="height:100vh">
		<view style="width:100vw;;height:45vh;background-color: white;margin: 0 auto;overflow-y: hidden;position: relative;"
		>
		
		
			<view style="width:100vw;height:90%;position: relative;z-index: 1;overflow-x: hidden;">
				<image :src="backvideo" style="width:100vw;height:100%;position: absolute;top:0;z-index: -1;" mode="aspectFill" 
				
				>
				<image>
				<view 
				v-if="backgroundnum>1"
				style="margin-right: 6vw;top:0;margin-top: 50px;right:0;position: absolute;color:white;font-size: 13px;z-index: 2;" 
				:style="{color:color1}"
				>
					<text style="" @click="changebackground">切换背景</text>
					<text style="margin-left:20px" @click="tohistory()">浏览记录</text>
				</view>
				<view style="width:92vw;margin-left: 3vw;;height:70%;position: absolute;top:20%;z-index: 2;">
					<view style="display: flex;flex-direction: row;align-items: center">
						<userhead :type="1" style="width:100px;height:100px; transform: scale(0.75);" :size="'100'" :username="username" :userheadimage="userheadimage" :headborder="headborder" :pianyi="pianyi"></userhead>
						<view style="width:40vw;margin-left:10px;"
						
						>
							<view style="width:100%;font-size:17px;font-weight: 700;" :style="{color:color1}">
								{{username}}
							</view>
							<view style="width:100%">
								<view style="display: flex;flex-direction: row;flex-wrap: warp;margin-top: 7px;margin-bottom:7px;color:white">
									<view style="height:10px;
									padding:3px;
									justify-content: center;
									display:flex;
									align-items:center;border-radius:20px;;padding-left:10px;padding-right:10px;"
									v-if="shenfen.length==0"  @click="toshenfen()"
									:style="{color:color4,backgroundColor:color3,border:color4+' solid 1px'}"
									>
										<text style="font-size:10px">添加身份标签</text>
									</view>
									<view v-for="(item,index) in shenfen" v-if="index==0" @click="toshenfen()">
										<view style="height:10px;
										padding:3px;
										justify-content: center;
										display:flex;
										align-items:center;border-radius:20px;;padding-left:10px;padding-right:10px;"
										:style="{color:color4,backgroundColor:color3,border:color4+' solid 1px'}"
										>
											<text style="font-size:10px">{{item.name}}</text>
										</view>
									</view>
								</view>
							</view>
							<view style="font-size: 12px;" :style="{color:color1}">
								UID：{{userid}}
							</view>
						</view>
					</view>
					<view style="width:50vw;display: flex;flex-direction: column; ;align-items: center;height:13px;margin-top:10px;margin-left:10px;">
						<view style="width:100%;margin-left:2px">
							
							<u--text :lines="1" :color="color1" size="13" :text="sign"  v-if="sign!=null" ></u--text>
							<u--text :lines="1"  :color="color1" size="13"  text="暂无签名"  v-if="sign==null"></u--text>
						</view>
					</view>
					<view style="width:50vw;display: flex;margin-top:15px;margin-left:10px;">
					
						<view style="display: flex;;margin-left:2px;padding:2px 5px 2px 5px;border-radius: 15px;"
							:style="{color:color4,backgroundColor:color3,border:color4+' solid 1px'}"
						>
							<text :style="{color:color1}" style="font-size: 11px;">{{'IP归属地:'+cname}}</text>
						</view>
					</view>
					<view style="width:100vw;display: flex;flex-direction: row;align-items: center;height:13px;margin-top:65px;margin-left:10px">
						<view style="width:35vw;display:flex;flex-direction:row;align-items:center;justify-content: center;font-size:12px;"
						:style="{color:color1}"
						>
							<view style="width:50px;display:flex;flex-direction:column;align-items:center"
							@click="toattention()"
							>
								<view >关注</view>
								<view >{{attention}}</view>
							</view>
							<view style="width:50px;display:flex;flex-direction:column;align-items:center;margin-left:20%;margin-right:20%"
							@click="tofans"
							>
								<text>粉丝</text>
								<text>{{fans}}</text>
							</view>
								<view style="width:50px;display:flex;flex-direction:column;align-items:center">
								<text>获赞</text>
								<text>{{bylike}}</text>
							</view>
						</view>
						<view style="margin-left:auto;margin-right:8vw;width:40vw;;display: flex;flex-direction:row;align-items: center;height:13px"
						:style="{color:color1}"
						>
							<view style="margin-left: auto;padding:5px 8px 5px 8px;border-radius: 15px;font-size: 13px;" 
							:style="{color:color4,backgroundColor:color3,border:color4+' solid 1px'}"
							@click="myinfo()">
								<text>我的信息</text>
							</view>
							<view style="margin-right:3vw;margin-left: 5vw;;font-size:15px;display:flex;flex-direction:row;padding:5px 10px 5px 10px;border-radius: 15px;align-items: center;justify-content: center"
							:style="{color:color4,backgroundColor:color3,border:color4+' solid 1px'}"
							 @click="setting()" 
							>
								<u-icon name="setting" size="17" :color="color1"></u-icon>
							</view>
						</view>
					</view>
				</view>
			</view>
		

			<view style="margin-top:-20px;position: absolute;bottom:0;width:100vw;height:10%;border-radius: 15px;background-color: white;justify-content: center;margin-bottom: 15px;display: flex;align-items: center;flex-direction:column;color:black;border-radius:15px 15px 0 0;z-index: 5;
			border-bottom: 0.5px solid #cdd2da;padding-bottom: 5px;font-size: 16px;
			"
			
			>
				<view style="width:50vw;display: flex;flex-direction: row;align-items: center;justify-content: center;">
					<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;">
						<text style="" v-if="selectpage==0">主题</text>
						<text style="color:#909399" v-if="selectpage!=0"
						@click="selectpage=0"
						>主题</text>

					</view>
					<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;margin-left:30px;margin-right:30px">
						<text style=""v-if="selectpage==1">点赞</text>
						<text style="color:#909399"v-if="selectpage!=1"
						@click="selectpage=1"
						>点赞</text>
					</view>
					<view style="margin-top: 5px;width:32px;display: flex;flex-direction: column;justify-content: center;">
						<text style=""v-if="selectpage==2">收藏</text>
						<text style="color:#909399"v-if="selectpage!=2"
						@click="selectpage=2"
						>收藏</text>
					</view>
				</view>
				
				<view style="100vw;display: flex;align-items: center;">
					<view style="width:50vw;display: flex;justify-content: center;">
					<view style="width:28px;height:2px;border-radius: 5px;margin-top: 5px;transition: 0.2s;"
					:style="{backgroundColor:skincolor}"
					:class="{'left1':selectpage==0,'left2':selectpage==2}"
					>
						
					</view>
					</view>
				</view>
			</view>
		</view>
		<view style="width:100vw;margin-top:-20px">
			<swiper duration="200" skip-hidden-item-layout style="width:100vw;height:100vh" :current="selectpage" @change="changeselectpage">
				<swiper-item style="width:100vw;display: flex;flex-direction: column;">
					<u-list style="height:100%;width:100%;background-size: cover;background-attachment: fixed;padding-bottom: 0vh;"  :scroll-y="true" @scrolltolower="getmoretheme"
					ref="list"
					:scrolly="false"
					>
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
						<view style="margin-bottom: 50px;" 	v-if="selectpage==0">
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
				</swiper-item>
				<swiper-item style="width:100vw;display: flex;flex-direction: column;">
					<u-list style="height:100%;width:100%;background-size: cover;background-attachment: fixed;padding-bottom: 0vh;"  :scroll-y="true" @scrolltolower="getmoretheme"
					ref="list1"
					:scrolly="false"
					>
					<view v-for="(item,index) in themelist1" style="width:100vw;z-index: 0;background-color:white"  v-if="themelist.length!=0">
					
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
						<view style="margin-bottom: 50px;"
						v-if="selectpage==1"
						>
							<u-loadmore
								    :status="status1" 
								    loading-text="努力加载中" 
								    loadmore-text="轻轻上拉" 
								    nomore-text="实在没有了" 
									fontSize="12"
									iconSize="14"
									style="margin-top:10px"
							/>
						</view>
					</u-list>
				</swiper-item>
				
				<swiper-item style="width:100vw;display: flex;flex-direction: column;">
					<u-list style="height:100%;width:100%;background-size: cover;background-attachment: fixed;padding-bottom: 0vh;"  :scroll-y="true" @scrolltolower="getmoretheme"
					ref="list2"	
					:scrolly="false"
					>
					<view v-for="(item,index) in themelist2" style="width:100vw;;z-index: 0;background-color:white"  v-if="themelist.length!=0">
					
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
						<view style="margin-bottom: 50px;" 	v-if="selectpage==2">
							<u-loadmore
								    :status="status2" 
								    loading-text="努力加载中" 
								    loadmore-text="轻轻上拉" 
								    nomore-text="实在没有了" 
									fontSize="12"
									iconSize="14"
									style="margin-top:10px"
							/>
						</view>
					</u-list>
				</swiper-item>
			</swiper>
			
		</view>
</u-list>
		
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
				selectpage:0,
				username:"",
				userheadimage:"",
				userbackgroundimage:"",
				userid:0,
				sign:"",
				color1:"black",
				toutu:"",
				status:"loading",
				status1:"loading",
				status2:"loading",
				show9:0,
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
				themelist1:[],
				themelist2:[],
				page1:0,
				page2:0,
				fanss:[],
				color3:"#ff006e",
				attentions:[],
				attentionlist:[],
				setWidth:0,
				setWidth1:0,
				shenfen:[],
				skincolor:"white",
				show:false,
				show1:false,
				show2:false,
				show4:false,
				show5:false,
				show8:false,
				show10:false,
				birthday:0,
				banreason:"",
				bantime:0,
				fanspage:0,
				attentionpage:0,
				fansfangdou:0,
				color4:"white",
				attentionfangdou:0,
				skinchoose:0,
				backvideo1:"",
				choosebackground:1,
				backgroundnum:1,
				likecolor:"#ff007f",
				fangdou1:0,
				fangdou2:0,
				cname:"",
			}
		},
		mounted() {
			let that=this;
			uni.request({
			    url:getApp().globalData.http+"/api/getipaddress",
				method:'POST',
				data:{
					
				},
				success: (res) => {
			      that.cname=res.data.data.address;
				  
				}
			})

			this.skinchoose=getApp().globalData.skinchoose;
			if(this.skinchoose!=0){
				this.skincolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.choosebackground=getApp().globalData.skin[getApp().globalData.skinchoose-1].choosebackground;
				this.backvideo=getApp().globalData.skin[getApp().globalData.skinchoose-1].backvideo[this.choosebackground];
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.backgroundnum=getApp().globalData.skin[getApp().globalData.skinchoose-1].backgroundnum;
				this.color3='';
				this.color4=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
			}
			this.getmyself();
			MiddleUtil.$on('getmyslef',(data)=> {
							this.getmyself();
			})
			uni.request({
				url:getApp().globalData.http+"/api/getmysavelist",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie,
					"userid":getApp().globalData.userid,
					"savepage":this.page2
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
						
						this.themelist2=res.data.data;
						if(res.data.data.length<5){
							
							this.fangdou2=1;
							this.page2=-1;
						}else{
							this.fangdou2=0;
							this.page2++;
						}
					}
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
					"likepage":this.page1
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
						this.themelist1=res.data.data;
						if(res.data.data.length<5){
							
							this.fangdou1=1;
						}else{
							this.fangdou1=0;
							this.page1++;
						}
					}
				}
			})
		},
		methods: {
			changebackground(){
				this.choosebackground++;
				if(this.choosebackground==this.backgroundnum)this.choosebackground=0;
				getApp().globalData.skin[getApp().globalData.skinchoose-1].choosebackground=this.choosebackground;
				uni.setStorage({
				    key: "skin",
				    data: getApp().globalData.skin,
				    success: function () {
				    }
				});
				this.backvideo=getApp().globalData.skin[getApp().globalData.skinchoose-1].backvideo[this.choosebackground];
			},
			myinfo(){
				uni.navigateTo({
					url:"/pages/index/myinfo/myinfo"
				})
			},
			changeselectpage(e){
				this.selectpage=e.target.current;
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
			scroll(e){
				if(e>=200&&e<280){
					this.show9=1;
				}
				else if(e>=280&&this.show9==1){
					this.show9=2;
					this.$refs.list.changey(true);
					this.$refs.list1.changey(true);
					this.$refs.list2.changey(true);
					
				}else if(e<200&&this.show9!=0) {
					this.show9=0;
					
					this.$refs.list.changey(false);
					
					this.$refs.list1.changey(false);
					
					this.$refs.list2.changey(false);
				}
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
			getmoretheme(){
				if(this.selectpage==0){
					this.getmoretheme1();
				}
				else if(this.selectpage==1){
					this.getmoretheme2();
				}
				else{
					this.getmoretheme3();
				}
			},
			getmoretheme2(){
				if(this.fangdou1==1)return this.fangdou1=1;
				uni.request({
					url:getApp().globalData.http+"/api/getmylikelist",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"likepage":this.page1
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
								this.themelist1.push(res.data.data[i]);
							}
							
						
							if(res.data.data.length<5){
								this.status1="nomore";
								this.fangdou1=1;
							}else{
								this.fangdou1=0;
								this.pag1e++;
							}
						}
					}
				})
			},
			getmoretheme3(){
				if(this.fangdou2==1)return;this.fangdou2=1;
				uni.request({
					url:getApp().globalData.http+"/api/getmysavelist",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"savepage":this.page2
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
								this.themelist2.push(res.data.data[i]);
							}
							if(res.data.data.length<5){
								this.status2="nomore";
								this.fangdou2=1;
								this.page2=-1;
							}else{
								this.fangdou2=0;
								this.page2++;
							}
						}
					}
				})
			},
			getmoretheme1:function(){
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
.op0{
	opacity: 0;
	z-index: -1;
}
.op1{
	opacity: 0;
	z-index: 11;
}
.op2{
	opacity: 1;
	z-index: 11;
}
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
.left1{
	transform: translateX(-62px);
}
.left2{
	transform: translateX(62px);
}
</style>
