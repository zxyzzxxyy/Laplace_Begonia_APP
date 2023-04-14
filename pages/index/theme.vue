<template>
<view style="background-color:white;height:100vh;width:100vw;padding-top: 0%;background-size: cover;background-attachment: fixed;overflow-y:hidden" >
	
	<view style="display: flex;flex-direction: row;padding-left:2.5vw;width:97.5vw;align-items: center;padding-top: 5vh;margin-bottom: 0px;padding-bottom: 10px;"
	:style="{backgroundColor:color}"
	>
	<view  style="display: flex;flex-direction: row;width:100%;align-items: center;"
	>
		<view style="display: flex;flex-direction: row;padding-bottom: 0px;margin-right:10px;height:30px;align-items: center;" @click="back">
		<u-icon name="arrow-left"  size="23" style="" :color="color1" ></u-icon>
		</view>
		<view style="display: flex;flex-direction: row;align-items: center;height:30px;width:100%">
			<view style="transition: 0.3s;display: flex;flex-direction: row;" :style="{Opacity:op2}" @click="heself(1)">
				<userhead :pianyi="{}" :headborder="''" style="margin-right:5px;z-index: 1;;width:30px;height:30px" :size="'30'" :username="username1" :userheadimage="userheadimage1" ></userhead>
				<u--text  size="16" :text="username1" lines="1" :color="color1"></u--text>
			</view>
			<view style="display: flex;flex-direction: row;margin-left: auto;margin-right:2vw">
			<view style="display: flex;flex-direction: row;margin-left: auto;align-items: center;" v-if="juge_admin()">
					
				<u-icon v-if="activity!=1" name="gift" :color="color1"  size="18" style="margin-left: 10px;" @click="setactivity()" ></u-icon>
				<u-icon v-if="activity==1" name="gift" color="#e45656" size="18" style="margin-left: 10px;"  @click="deleteactivity()"></u-icon>
					
			</view>
			<view style="display: flex;flex-direction: row;margin-left: auto;align-items: center;" v-if="juge_admin()">
				
				<u-icon v-if="jing!=1" name="integral" :color="color1"  size="18" style="margin-left: 10px;" @click="setjing()" ></u-icon>
				<u-icon v-if="jing==1" name="integral" color="#e45656" size="18" style="margin-left: 10px;"  @click="deletejing()"></u-icon>
				
			</view>
			<view style="display: flex;flex-direction: row;;align-items: center;" v-if="juge_admin()">
				
				<u-icon  @click="settop()"  v-if="top!=1" :color="color1"  name="arrow-up-fill"  size="18" style="margin-left: 10px;" ></u-icon>
				<u-icon  @click="deletetop()" v-if="top==1" color="#f9ae3d"  name="arrow-up-fill"  size="18" style="margin-left: 10px;" ></u-icon>
			</view>
			<u-icon name="trash"  size="18"  :color="color1"  style="margin-left: 10px;" v-show="juge()"></u-icon>
			<text style="font-size: 14px;" :style="{color:color1}" @click="show=true" v-show="juge()">删除</text>
			</view>
		</view>
	</view>
	<!--
	<view style="display: flex;flex-direction: row;align-items: center;margin-left: auto;margin-right: 2.5vw;">
	<u-icon name="trash"  size="20" style="margin-left: 20px;" v-show="juge()"></u-icon>
	<text style="font-size: 16px;color:#8f8f8f" @click="show=true" v-show="juge()">删除</text>
	</view>
	-->
	</view>
		
		<scroll-view :scroll-y="true" style="height:100vh;z-index: -1;"
		 @scroll="scroll1" 
		 :scroll-into-view="scroll_top1"
		 scroll-with-animation="true"
		  @scrolltolower="getmorereply()" >
		<view style="width:100%;display: flex;flex-direction: column;align-items: center;background-color: white;z-index: 1;padding-bottom: 0%;background-size: cover;background-attachment: fixed;height:100vh" 
		
		>
		<view style="width:100%;background-color: white;height:auto;padding-bottom: 1%;padding-top: 0%;border-radius: 10px;"
		>
			
			<view style="display: flex;flex-direction: row;margin-bottom: 20px;align-items: center;margin-top:10px;width:95vw;padding-left: 2.5vw;padding-right: 2.5vw;"  v-if="createtime!=0">
				<u-tag :text="fenlei"  plain plainFill    style="margin-right: 10px;" v-if="themeid!=0"></u-tag>
				<u-tag text="精华"  plain plainFill  v-if="jing==1" type="error" style="margin-right: 10px;"></u-tag>
				<view style="">
				<u-tag text="原创"  plain plainFill  v-if="type==0" type="warning"></u-tag>
				<u-tag text="搬运"  plain plainFill  v-if="type==1" type="warning"></u-tag>
				</view>
				
				

			</view>
			<view style="width: 95vw;overflow-x: hidden;border-radius: 3px;"  v-if="show2">
			<u-skeleton
				    rows="0"
					:avatar="true"
					:title="true"
					style="margin-left:2.5vw;margin-top: 5vh;"
					avatarSize="40"
					
				/>
				<u-skeleton
					    rows="1"
						
						rowsHeight="20px"
						:title="false"
						style="margin-left:2.5vw;margin-top: 20px;"
					
						
					/>
					<br>
				<u-skeleton
					    rows="1"
						
						rowsHeight="400px"
						:title="false"
						style="margin-left:2.5vw;margin-top: 20px;"
					
			
					/>
			</view>
			<view v-if="!show2" >
				<view style="width: 95vw;padding-left:2.5vw;padding-right:2.5vw;display: flex;flex-direction: row;;
				margin-left: 0%;
				" >
				
					<view style="margin-right: 5px;height:38px;display: flex;"  @click="heself()">
				<userhead style="z-index: 1;;width:40px;height:40px" :size="'40'" :username="username1" :userheadimage="userheadimage1" :headborder="headborder" :pianyi="pianyi"></userhead>
				</view>
					<view style="height:38px;display: flex;flex-direction: column;margin-left: 0px;margin-bottom: 10px;width: 100%;">
						
						<view style="display: flex;flex-direction: row;">
							<view style="display: flex;flex-direction: column; width:100%;margin-left: 5px;">
								<view style="display: flex;flex-direction: row;align-items: center;">
								<text style="margin-right: 5px;font-size: 16px;">{{username1}}</text><text style="font-size: 15px;" v-if="shenfen.length!=0">·</text><text style="margin-left:5px;font-size: 14px;color:#909399" v-if="shenfen.length!=0">{{shenfen}}</text>
								
								</view>
								<view style="display: flex;flex-direction: row;align-items: center;margin-left: 0px;">
									<text style="font-size: 12px;color:#838383;margin-right: 5px;">{{time(createtime)}}</text>
									
								</view>
								
							</view>
							
							<view style="margin-left: auto;" v-if="jugemyself()">
							<view style="width:70px;height:32px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 14px;"  v-show="jugelogin()&&!jugeattention()" @click="addattention()">关注TA</view>
							<view style="width:70px;height:32px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 14px;"  v-show="jugelogin()&&jugeattention()" @click="deleteattention()">已关注</view>
							
							</view>
						</view>
					</view>
		
				</view>
			</view>
			
			<view style="width:95vw;display: flex;padding-right:2.5vw;padding-left: 2.5vw;">
			<text style="user-select:text;font-size: 20px;font-weight: 700;">{{title}}</text>
			</view>
			<view style="width:100%;display: flex;align-items: center;justify-content: center;">
			<!--	<text style="user-select:text;font-size: 25px;font-weight: 700;">{{title}}</text>-->
				</view>

			<mp-html 
			:content="jugeemoji(article)" 
			style="margin-top:15px;width:95vw;padding-left:2.5vw;padding-right: 2.5vw;font-size: 15px;"
			class="mp"
			:img-cache="false"
			:show-img-menu="false"
			/>
			<br>
			<view style="margin-left: 2vw;margin-bottom:20px">
			<u--text @click="weizhi" prefixIcon="map-fill" :text="position" v-if="position!=''" color="#3c9cff" iconStyle="color:#3c9cff;margin-right:5px"></u--text>
			</view>
			<view style="display: flex;flex-direction: row;padding-left: 2.5vw;padding-right: 2.5vw;width: 95vw;flex-wrap: wrap;">
			<u-tag v-for="(item,index) in tags" borderColor="#ecf5ff" :text="item"  style="width: auto;border:none;margin-right:10px;margin-bottom: 10px;" plain plainFill @click="linktag(item)"></u-tag>
			</view>
			<view style="margin-top: 20px;padding-left: 2.5vw;padding-right: 2.5vw;width: 95vw;" v-if="type==1">

				<text style="font-size:15px;font-weight: 700;">原文链接:</text>
				<br>
				<text @click="linkto()"  style="font-size:15px;white-space;word-break: break-all;color:#3c9cff">{{ycsrc}}</text>
			</view>
			
			
		</view>				
		<view style="margin-top:10px;margin-bottom:10px;width:100%;height:10px">
		<u-gap  height="5" style="width:100%;" bgColor="#f4f4f4"></u-gap>
		</view>
		
		<view style="width:95vw;background-color: white;height:auto;padding-left:5vw;padding-right: 5vw;padding-bottom: 1%;padding-top: 1%;margin-top: 0px;"
		 v-show="createtime>0"
		>
			<view style="">
				<view style="width: 100%;display: flex;flex-direction: row;">
					<text style="font-size: 15px;">共{{replyslength}}条评论</text>
					<text style="font-size: 14px;margin-left: auto;" v-if="replytype==2" @click="getreply(1)">全部回复</text>
					<text style="font-size: 14px;margin-left: auto;font-weight: 700;" v-if="replytype==1"  @click="getreply(1)">全部回复</text>
					<text style="font-size: 14px;margin-left: 10px"  v-if="replytype!=2"  @click="getreply(2)">只看作者</text>
					<text style="font-size: 14px;margin-left: 10px;font-weight: 700"  v-if="replytype!=1" @click="getreply(2)">只看作者</text>
				</view>
				
					
			</view>
		</view>
	
		<view style="width:95vw;background-color: white;height:auto;padding-left:5vw;padding-right: 5vw;padding-bottom: 1%;padding-top: 1%;margin-top: 0px;"
		 v-show="createtime>0"
		>
			
			<view v-for="(item,index) in replys" style="width:100%;margin-top: 10px;margin-bottom: 10px;" :id="'a'+item.id">
				<view style="display: flex;flex-direction: row;width:100vw;;align-items:center">
					<view style="margin-right: 10px;height:50px;display: flex;align-items:center"  @click="heself1(item.userid)">
					<userhead style="z-index: 1;;width:36px;height:36px" :size="'36'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>
					</view>
					<view style="height:50px;display: flex;flex-direction: column;justify-content: center;">
					<view style="display: flex;flex-direction: row;align-items: center;">
					<view style="display: flex;flex-direction: row;align-items: center;width:88vw">
					<view style="width:auto;display: flex;flex-direction: row;margin-right:5px">
					<text style="margin-right: 5px;font-size:14px;font-weight: 500;">{{item.username}}</text><text style="font-size: 14px;margin-right:5px" v-if="item.shenfen.length!=0">·</text><u--text :text="item.shenfen" size="13px" color="#909399" :lines="1" v-if="item.shenfen.length!=0"></u--text>
					</view>
						<view  v-if="zuozhe(item.userid)" style="flex-direction: row;font-size:12px;padding:1.5px;;margin-right:5px;height:16px;width:30px;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:#ffffff;background-color: #3c9cff;">作者</view>
					<view  style="margin-left: auto;margin-right: 5vw;" 
>
						<u-icon @click="deletereply(item)" color="#c8c9cc" name="more-dot-fill" size="16" style="transform:rotate(90deg)">
							
						</u-icon>
						
					</view>

					</view>
					</view>
						<view style="display: flex;flex-direction: row;">
							<text style="font-size: 12px;color:#909399;margin-right: 5px;">{{item.louceng}}楼</text>
							<text style="font-size: 12px;color:#909399;" >{{time1(item.time)}}</text>
						</view>
					</view>
					
				</view>
				<view @click.self="test(item)" style="display: flex;flex-direction: column;justify-content: center;margin-left: 2.5%;width:80vw" >
					
					
					<view style="border-radius: 5px;width:100%;margin-left:38px;padding-top: 0px;padding-bottom: 0px;margin-top: 0px;" v-if="item.data!=''" @click="test(item)" >
						<!--<text style="font-size: 14px;user-select:text">{{item.data}}</text>-->
						<mp-html
						:content="jugeemoji(item.data)" 
						style="font-size: 15px;"
						class="mp"
						loading-img="/static/white.jpg"
						:img-cache="false"
						:show-img-menu="false"
						/>
					</view>
					<view  v-if="item.image.length>5" style="margin-top:10px;margin-left:38px;width:100%;display:flex;direction:row;margin-bottom:5px"  >
						<view >
						<u-album  :urls="imagesrc(item.image)" :singleSize="setWidth" :multipleSize="setWidth1"></u-album>
						</view>
					</view>
					<view style="margin-top:10px;margin-left:38px">
					<u--text :lines="2" :text="item.sign" color="#909399" v-if="item.sign.length>0" size="12"></u--text>
					</view>
					<view style="margin-bottom:5px;margin-top: 10px;width:100%;margin-left:38px;display:flex;justify-content:center" v-if="item.loucengreply.length>0" @click="test(item)">
						<view style="width:95%;background-color:#f6f6fc;border-radius:5px;padding-left:2.5%;padding-right:2.5%;padding-top:5px;padding-bottom:5px">
							<view v-for="(item1,index1) in item.loucengreply" v-if="index1<3">
								<u--text :lines="1" :text="test2(item1)" color="#73757a"  size="14"></u--text>	
							</view>
							<text style="font-size: 14px;color:#3c9cff">查看全部{{item.loucengreply.length}}条回复</text>
						</view>
				
					</view>
					
				</view>
				<view style="margin-top:5px;margin-bottom:5px;margin-left: 45px;max-width:85%;border-top: 1px solid #f4f4f4;height:1px">
					
				</view>
				
			</view>
			<view style="padding-bottom:7vh;width: 100%;display: flex;flex-direction: row;align-items: center;justify-content: center;font-size: 15px;color:#787878;;margin-top:0px;"
				:class="{'bottom1':jugelogin1,'bottom2':!jugelogin1}"
			>
				<u-loadmore
					    :status="status" 
					    loading-text="努力加载中" 
					    loadmore-text="轻轻上拉" 
					    nomore-text="实在没有了" 
						fontSize="12"
						iconSize="14"
						style="margin-bottom: 15px;"
				>
				</u-loadmore>
				
			</view>

		</view>
		</view>
		
		</scroll-view>
		
		<view >
				<u-modal :show="show" title="删除主题" content="是否删除主题?" showCancelButton
				@cancel="show=false" @confirm="delete_theme()" :closeOnClickOverlay="true"
				@close="show=false" 
				></u-modal>
		</view>
		<view >
				<u-modal :show="show1" title="删除主题" content="是否删除回复?" showCancelButton
				@cancel="show1=false" @confirm="deletereply1()" :closeOnClickOverlay="true"
				@close="show1=false" 
				></u-modal>
		</view>
		<view>
				<u-toast ref="uToast"></u-toast>
				
		</view>
		<u-popup :show="show3" mode="bottom"  @close="show3=false,replydata='',test1" :round="15" >
		        <view style="height:90vh;padding-top:2vh" >
					<view style="height:2%;width:100vw;display:flex;flex-direction:row;align-items:center;margin-left:2.5vw"
					>
						<view style="width:20px" @click="show3=false,replydata=''">
							<u-icon name="close" color="#000000" size="20"></u-icon>
						</view>
						<view style="height:5%;width:100vw;display:flex;justify-content:center;align-items:center;margin-left:-20px">
						<text>{{item.louceng}}楼的回复</text>
						</view>
					</view>
					<u-divider width="100vw"></u-divider>
					
					<view style="height:95%;overflow-y:auto;width:97.5vw;overflow-x:hidden">
		            <view style="display: flex;flex-direction: row;width:97.5vw;overflow-y:auto" v-if="show3==true">
		            	<view style="margin-right: 10px;height:50px;display: flex;align-items:center"  @click="heself1(item.userid)">
		            	<userhead style="padding-left: 2.5vw;z-index: 1;;width:40px;height:40px" :size="'40'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>
		            	</view>
		            	<view style="height:50px;display: flex;flex-direction: column;justify-content: center;">
		            	<view style="display: flex;flex-direction: row;align-items: center;">
		            	<view style="display: flex;flex-direction: row;align-items: center;">
						<view style="width:auto;display: flex;flex-direction: row;margin-right:5px">
						<text style="margin-right: 5px;font-size:14px;font-weight: 500;">{{item.username}}</text><text style="font-size: 14px;margin-right:5px" v-if="item.shenfen.length!=0">·</text><u--text :text="item.shenfen" size="13px" color="#909399" :lines="1" v-if="item.shenfen.length!=0"></u--text>
						</view>						
		            	</view>
						<view  v-if="zuozhe(item.userid)" style="flex-direction: row;font-size:12px;padding:2px;;margin-right:5px;height:16px;width:30px;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:#ffffff;background-color: #3c9cff;">作者</view>
		            	</view>
		            	<text style="font-size: 12px;color:#909399;">{{time1(item.time)}}</text>
		            	</view>
		            	
		            </view>
					<view style="display: flex;flex-direction: column;justify-content: center;margin-left: 10px;width:97.5vw;" @click="test(item)">
						
						
						<view style="border-radius: 5px;width:80%;padding-top: 0px;padding-bottom: 0px;margin-top: 5px;margin-left:38px" v-if="item.data!=''">
							<!--<text style="font-size: 14px;user-select:text">{{item.data}}</text>-->
							<mp-html
							:content="jugeemoji(item.data)" 
							style="font-size: 14px;margin-left:2.5vw"
							class="mp"
							:img-cache="false"
							:show-img-menu="false"
							/>
						</view>
						<view style="margin-top: 10px;margin-left:38px">
							<u-album style="margin-left:2.5vw" :urls="imagesrc(item.image)" :multipleSize="setWidth1"></u-album>
						</view>
						<view style="margin-left: 38px;font-size: 12px;color:#909399;margin-top: 10px;width:80%">
							<view style="margin-left:2.5vw">
							<u--text  :lines="2" :text="item.sign" color="#909399" v-if="item.sign!=''&&item.sign!=''" size="12"></u--text>
							</view>
							<view style="height:5px" v-if="item.sign!=null&&item.sign!=''"></view>
							<view style='margin-left:2.5vw'>
							<text >{{item.louceng}}楼</text>
							</view>
						</view>
						
					</view>
				<view style="width: 95vw;display:flex;justify-content:center;">
				<u-divider text="" style="width: 100%;"></u-divider>
				
				</view>
				<view style="margin-bottom: 10px;">
				<text style="margin-left:2.5vw;" v-if="item.loucengreply!=null">{{item.loucengreply.length}}条回复</text>
				</view>
				<view v-for="(item,index) in item.loucengreply" style="margin-left:2.5vw"
			
				>
					<view style="display: flex;flex-direction: row;width:50%;" v-if="show3==true">
						<view style=";margin-right: 10px;height:50px;display: flex;align-items:center"  @click="heself1(item.userid)">
							<userhead style="z-index: 1;;width:40px;height:40px" :size="'40'" :username="item.username" :userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi"></userhead>
						</view>
						<view style="height:50px;display: flex;flex-direction: column;justify-content: center;"
						@click="setloucengreplyat(item)"
					
						>
							<view style="display: flex;flex-direction: row;align-items: center;">
						<view style="display: flex;flex-direction: row;align-items: center;width:90vw">
						<view style="width:auto;display: flex;flex-direction: row;margin-right:5px"
					
						>
						<text style="margin-right: 5px;font-size:14px;font-weight: 500;"
						>{{item.username}}</text><text style="font-size: 14px;margin-right:5px" v-if="item.shenfen.length!=0">·</text><u--text :text="item.shenfen" size="13px" color="#909399" :lines="1" v-if="item.shenfen.length!=0"></u--text>
						</view>
						<view  v-if="zuozhe(item.userid)" style="flex-direction: row;font-size:12px;padding:2px;;margin-right:5px;height:16px;width:30px;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:#ffffff;background-color: #3c9cff;">作者</view>
						<view  style="margin-left: auto;margin-right: 10vw;" v-show="jugeuserid(item.userid)"
						@click="deletereplylouceng(item.id)">
							<u-icon name="close"  size="15" 
							></u-icon>
						</view>							
						</view>
						</view>
						<text style="font-size: 12px;color:#909399;">{{time1(item.time)}}</text>
						</view>
						
					</view>
					<view style="display: flex;flex-direction: column;justify-content: center;margin-left: 10px;width: 100%;"
				
					>
						
						
						<view style="border-radius: 5px;width:80%;margin-left:38px;padding-top: 0px;padding-bottom: 0px;margin-top: 5px;" v-if="item.data!=''"
							@click.prevent="setloucengreplyat(item)"
							@click.self="setloucengreplyat(item)"
						>
							<view v-if="item.atid!=null&&item.atid!=undefined&&item.atid!=0" style="font-size: 14px;">
								回复
								<text @click="heself1(item.atuserid)" style="margin-left:5px;color:#3c9cff">{{'@'+item.atusername+''}}</text>
							</view>
							<mp-html
						
							:content="jugeemoji(item.data)" 
							style="font-size: 14px;min-width:100%"
							class="mp"
							:img-cache="false"
							:show-img-menu="false"
							
							/>
						</view>
						<view style="margin-left: 0px;font-size: 12px;color:#909399;margin-top: 10px;width:80%;margin-left:38px">
						<u--text :lines="2" :text="item.sign" color="#909399" v-if="item.sign!=''&&item.sign!=''" size="12"></u--text>
						<view style="height:5px" v-if="item.sign!=null&&item.sign!=''"></view>
						<u-divider width="80vw"></u-divider>
					</view>
						
					</view>
					
				</view>
				<view style="height:70px;width:100vw;display:flex;justify-content:center">
					<text style="font-size: 14px;">没有更多了</text>
				</view>
				<view style="width:100vw;height:50px;opacity: 0;" v-if="jugelogin()">
					<text>1</text>
				</view>
				</view>
				<view style="min-height:6vh;position: fixed;bottom:0px;;z-index: 2;background-color:white;width:100vw;;
				border-top:0.5px solid #ebeff8;border-left:none;border-right:none;border-bottom:none;display:flex;align-items: center;
				;;flex-direction: column;justify-content: center;" :style="{marginBottom:keyborde+'px'}" v-if="jugelogin()"
				:class="{'s1':loucengreplyat.userid!=0}"
				>
					<view style="width:98%;padding:2%;;margin-right:3%;margin-left: 2%;"v-if="loucengreplyat.userid!=0">
						<view style="margin-left:38px">
							
							<u--text color="#909399" size="12" lines="1" :text="'回复'+' '+loucengreplyat.username+':'+loucengreplyat.data "></u--text>
						</view>
					</view>
					
					<view style="display: flex;flex-direction: row;width:100%;margin-left:4vw;align-items: center;"
					:style="{marginTop:height3?'10px':'0px'}"
					>
					<u-avatar mode="aspectFill" :src="myuserheadimage" v-if="myuserheadimage!=''" size="36"></u-avatar>
					<u-avatar :text="myusername.substr(0,1)"  randomBgColor v-if="myuserheadimage==''" size="36"></u-avatar>
					<view style="width:59%;margin-left:2vw;border-radius: 20px;margin-bottom: 0px;" 	>
					<u--textarea
						@blur="deletefocus()"
					    placeholder="说点什么..."
					    border="none"
					    v-model="replydata"
					    width="100%"
						shape="circle"
						height="18"
						style="background-color: #f6f7f8;border-radius: 20px;"
						:focus="autofocus"
						:adjust-position="false"
						@focus="height3=0"
					  ></u--textarea>
					</view>
					<view
					@click="height3=!height3"
					style="margin-left: 1.5%;"
					>
					<u-icon
					
					 color="#909399" name="more-circle"  size="32">
					 </u-icon>
					 </view>
					<view style="height:32px;width:15%;margin-top:0px;margin-left:1.5%;;border-radius:100px;background-color:#806aff;display:flex;align-items:center;justify-content:center" 
					@click="replylouceng()"
					>
						<text style="font-size: 16px;color:white;">回复</text>
					</view>
					</view>
					<view v-if="height3&&jugelogin()" style="width:100vw;height:300px;position: relative;background-color: #f6f7f8;margin-top: 10px;"
					>
						<swiper class="swiper" style="height:250px;;margin-bottom: 50px;"
						:current="emojiselect" circular
						@change="changeemojiselect"
						>
							<swiper-item v-for="(item,index2) in emoji">
								<view
									style="height:240px;overflow-y: auto;display: flex;flex-direction: row;flex-wrap: wrap;"
								>
									<image :src="item"  v-for="(item,index) in emojilist[index2]"
										style="width:16vw;height:16vw;margin-top:10px;margin-bottom:10px;margin-left: 2vw;margin-right: 2vw;" 
										mode="aspectFill"
										@click="addemoji(index,1)"
									>
												
									</image>
								</view>
							</swiper-item>								
						</swiper>
					
						<view style="position: absolute;width:100%;bottom: 0;height:60px;background-color: white;display:flex;flex-direction:row;overflow-x:auto">
							<view
							 :style="{marginLeft:index==0?'5vw':'0vw'}"
							 :class="{'selectemoji':emojiselect==index}"
							 v-for="(item,index) in emoji" style="width:60px;height:60px;margin-left:2vw;display: flex;align-items: center;justify-content: center;">
							<image @click="emojiselect=index"
							
							 style="width:40px;height:40px;margin-top:0px;margin-bottom:0px;" mode="aspectFill"
								:src="emoji[index].icon"
							>
								
							</image>
							</view>
						</view>
					</view>
				</view>
		    </view>
		</u-popup>
		<view style="position: fixed;bottom:0;width:100vw;;background-color: white;z-index: 3;display: flex;align-items: center;flex-direction: column;
		border-top:0.5px solid #ebeff8;min-height:6vh;align-items: center;justify-content: center;"
		v-if="jugelogin()">

		<view style="display: flex;flex-direction: row;width:100%;padding:2%;padding-top: 0;padding-bottom: 0;"
		:style="{marginTop:keyborde>0||height2||imageclick?(keyborde-(keyborde-10))+'px':'0px'}"
		
		>
				<userhead headborder="" :pianyi="{}" style="z-index: 1;margin-top:2px;margin-left:2%;width:34px;height:34px" :size="'34'" :username="username" :userheadimage="userheadimage" ></userhead>
				
				<u-textarea  style="width:66%;;margin-left:2%;border:1px solid #f6f7f8;
				border-radius: 20px;
				background-color: #f6f7f8;
				
				"
				maxlength="500"
				v-model="reply"
				 type="text" 
				 :adjust-position="false"
				placeholder="说点什么..."
				  :height="textarea1"
				border="none"
				@focus="show4=1,height2=0"
				@blur="show4=0"
				 ></u-textarea>

				<view  @click="huifu(1)" v-if="show4==1" style="height:34px;width:15%;margin-left:2.5%;margin-right:2.5%;border-radius:100px;background-color:#806aff;display:flex;align-items:center;justify-content:center">
					<text style="font-size: 16px;color:white;">回复</text>
				</view>
				<view v-if="show4==0" style="display: flex;flex-direction: row;margin-left:1.5%;align-items: center;margin-right:1%">
					<view style="display: flex;flex-direction: row;align-items: center;">
						<u-icon color="#000000" name="share"  size="26" style="margin-right: 3px;"></u-icon>
									
					</view>
					<view v-show="saveshow==0" @click="saveadd()" style="display: flex;align-items: center;height:100%">
						<u-icon name="star" color="#000000" size="26" style="margin-right: 3px;"></u-icon>
					
					</view>
					<view v-show="saveshow==1"  @click="savedelete()" style="display: flex;align-items: center;height:100%">
						<u-icon name="star"  size="26" style="margin-right: 3px;" color="#f9ae3d"></u-icon>
					
					</view>
				
					<view style="display: flex;flex-direction: row;align-items: center;" v-show="!jugelike(themeid)"
					@click="setlike(themeid)"
					> 
						<u-icon  labelSize="10"  space="1" name="heart" color="#000000" size="26" style="margin-right: 3px;"></u-icon>
								
					</view>
					<view style="display: flex;flex-direction: row;align-items: center;" v-show="jugelike(themeid)"
					@click="deletelike(themeid)"
					>
						<u-icon labelSize="10"  space="1" name="heart-fill" :color="likecolor"  size="26" style="margin-right: 3px;" ></u-icon>
					
					</view>
				</view>
			</view>
			<view 
			:style="{marginBottom:keyborde+'px'}"
			style="width:100vw;height:auto;display:flex;flex-direction: column;align-items: center;;" v-if="keyborde!=0||uploadimages.length>0||height2||imageclick==1">
				<view style="width:100vw;height:40px;display: flex;flex-direction: row;align-items: center;margin-bottom:0px">
					<u-icon
					 @click="height2=!height2,imageclick=0"
					 color="#909399" name="more-circle"  size="30" style="margin-left:3%;"></u-icon>
					
					<u-icon name="photo" color="#2979ff" size="35" v-if="uploadimages.length>0" style="margin-left:3%"
					@click="imageclick=!imageclick,height2=0;"
					></u-icon>
					<u-icon name="photo" color="#909399" size="35" v-if="uploadimages.length==0" style="margin-left:3%"
					@click="imageclick=!imageclick,test4(),height2=0"
					></u-icon>
				</view>
				 <scroll-view scroll-x="true" 
				 style="height:auto;	
				 white-space: nowrap;	width:100%;margin-left:2%		;
				 " :enable-flex="true"
				 v-if="imageclick==1">
				<image  v-for="(item,index) in uploadimages" :src="item"
					@click="deleteimage(index)" mode="aspectFill" 
					style="display: inline-block;
					height:15vw;width:15vw;margin-right:1vw;margin-left: 1vw;;border-radius: 15px;">
				</image>
				<view style="display: inline-block;overflow: hidden">
					<view
					@click="uploadimage()"
					style="
						background-color: #f6faff;
						height:15vw;width:15vw;vertical-align:top
						border-radius: 15px;
						display: flex;flex-direction: column;align-items: center;justify-content:center;
						margin-right:1vw;margin-left: 1vw;
						">
						<u-icon name="plus" color="#909399" size="26"></u-icon>
						<text style="color:#909399;font-size:12px">上传图片</text>
					</view>	
				</view>
				</scroll-view>
			</view>
			
			<view v-if="height2&&jugelogin()" style="width:100vw;height:300px;position: relative;background-color: #f6f7f8;margin-top: 10px;"
			>
				<swiper class="swiper" style="height:250px;;margin-bottom: 50px;"
				:current="emojiselect" circular
				@change="changeemojiselect"
				>
					<swiper-item v-for="(item,index2) in emoji">
						<view
							style="height:240px;overflow-y: auto;display: flex;flex-direction: row;flex-wrap: wrap;"
						>
							<image :src="item"  v-for="(item,index) in emojilist[index2]"
								style="width:16vw;height:16vw;margin-top:10px;margin-bottom:10px;margin-left: 2vw;margin-right: 2vw;" 
								mode="aspectFill"
								@click="addemoji(index,0)"
							>
										
							</image>
						</view>
					</swiper-item>								
				</swiper>
			
				<view style="position: absolute;width:100%;bottom: 0;height:60px;background-color: white;display:flex;flex-direction:row;overflow-x:auto">
					<view
					 :style="{marginLeft:index==0?'5vw':'0vw'}"
					 :class="{'selectemoji':emojiselect==index}"
					 v-for="(item,index) in emoji" style="width:60px;height:60px;margin-left:2vw;display: flex;align-items: center;justify-content: center;">
					<image @click="emojiselect=index"
					
					 style="width:40px;height:40px;margin-top:0px;margin-bottom:0px;" mode="aspectFill"
						:src="emoji[index].icon"
					>
						
					</image>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>

	import emoji from "../../components/thegithubs-vue2-emoji-editor/EmojiComponent.vue"
	import userhead from "@/pages/index/userhead/userhead.vue"
	export default {
		components:{
			userhead,emoji
		},
		data() {
			return {
				height3:0,
				emojiselect:0,
				emoji:[
					{
						"text":"Monaka",
						"icon":"/static/mnk/mnk_16.png",
						"type":"png"
					},
					{
						"text":"Monaka",
						"icon":"/static/mnk/mnk_32.jpg",
						"type":"jpg"
					},
					{
						"text":"Taffy",
						"icon":"/static/taffy/taffy_3.png",
						"type":"png"
					},
					{
						"text":"明前奶绿",
						"icon":"/static/mqnl/mqnl_9.png"
					}
				],
				emojilist:[
					[
					"/static/mnk/mnk_1.png",
					"/static/mnk/mnk_2.png",
					"/static/mnk/mnk_3.png",
					"/static/mnk/mnk_4.png",
					"/static/mnk/mnk_5.png",
					"/static/mnk/mnk_6.png",
					"/static/mnk/mnk_7.png",
					"/static/mnk/mnk_8.png",
					"/static/mnk/mnk_9.png",
					"/static/mnk/mnk_10.png",
					"/static/mnk/mnk_11.png",
					"/static/mnk/mnk_12.png",
					"/static/mnk/mnk_13.png",
					"/static/mnk/mnk_14.png",
					"/static/mnk/mnk_15.png",
					"/static/mnk/mnk_16.png",
					"/static/mnk/mnk_17.png",
					"/static/mnk/mnk_18.png",
					"/static/mnk/mnk_19.png",
					"/static/mnk/mnk_20.png",
					"/static/mnk/mnk_21.png",
					"/static/mnk/mnk_22.png",
					"/static/mnk/mnk_23.png",
					"/static/mnk/mnk_24.png",
					"/static/mnk/mnk_25.png",
					"/static/mnk/mnk_26.png",
					"/static/mnk/mnk_27.png",
					"/static/mnk/mnk_28.png",
					"/static/mnk/mnk_29.png",
					"/static/mnk/mnk_40.png",
					"/static/mnk/mnk_41.png",
					"/static/mnk/mnk_42.png",
					"/static/mnk/mnk_43.png",
					"/static/mnk/mnk_44.png",
					"/static/mnk/mnk_45.png",
					"/static/mnk/mnk_46.png",
					"/static/mnk/mnk_47.png",
					"/static/mnk/mnk_48.png",
					],
					[
					"/static/mnk/mnk_30.jpg",
					"/static/mnk/mnk_31.jpg",
					"/static/mnk/mnk_32.jpg",
					"/static/mnk/mnk_33.jpg",
					"/static/mnk/mnk_34.jpg",
					"/static/mnk/mnk_35.jpg",
					"/static/mnk/mnk_36.jpg",
					"/static/mnk/mnk_37.jpg",
					"/static/mnk/mnk_38.jpg",
					"/static/mnk/mnk_39.jpg",
					],
					[
					"/static/taffy/taffy_1.png",
					"/static/taffy/taffy_2.png",
					"/static/taffy/taffy_3.png",
					"/static/taffy/taffy_4.png",
					"/static/taffy/taffy_5.png",
					"/static/taffy/taffy_6.png",
					"/static/taffy/taffy_7.png",
					"/static/taffy/taffy_8.png",
					"/static/taffy/taffy_9.png",
					"/static/taffy/taffy_10.png",
					"/static/taffy/taffy_11.png",
					"/static/taffy/taffy_12.png",
					"/static/taffy/taffy_13.png",
					"/static/taffy/taffy_14.png",
					"/static/taffy/taffy_15.png",
					"/static/taffy/taffy_16.png",
					"/static/taffy/taffy_17.png",
					"/static/taffy/taffy_18.png",
					"/static/taffy/taffy_19.png",
					"/static/taffy/taffy_20.png",
					"/static/taffy/taffy_21.png",
					"/static/taffy/taffy_22.png",
					"/static/taffy/taffy_23.png",
					"/static/taffy/taffy_24.png",
					"/static/taffy/taffy_25.png",
					"/static/taffy/taffy_26.png",
					"/static/taffy/taffy_27.png",
					"/static/taffy/taffy_28.png",
					"/static/taffy/taffy_29.png",
					"/static/taffy/taffy_30.png",
					"/static/taffy/taffy_31.png",
					"/static/taffy/taffy_32.png",
					"/static/taffy/taffy_33.png",
					"/static/taffy/taffy_34.png",
					"/static/taffy/taffy_35.png",
					],
					[
						"/static/mqnl/mqnl_1.png",
						"/static/mqnl/mqnl_2.png",
						"/static/mqnl/mqnl_3.png",
						"/static/mqnl/mqnl_4.png",
						"/static/mqnl/mqnl_5.png",
						"/static/mqnl/mqnl_6.png",
						"/static/mqnl/mqnl_7.png",
						"/static/mqnl/mqnl_8.png",
						"/static/mqnl/mqnl_9.png",
						"/static/mqnl/mqnl_10.png",
						"/static/mqnl/mqnl_11.png",
						"/static/mqnl/mqnl_12.png",
						"/static/mqnl/mqnl_13.png",
						"/static/mqnl/mqnl_14.png",
						"/static/mqnl/mqnl_15.png",
						"/static/mqnl/mqnl_16.png",
						"/static/mqnl/mqnl_17.png",
						"/static/mqnl/mqnl_18.png",
						"/static/mqnl/mqnl_19.png",
						"/static/mqnl/mqnl_20.png",
						"/static/mqnl/mqnl_21.png",
						"/static/mqnl/mqnl_22.png",
						"/static/mqnl/mqnl_23.png",
						"/static/mqnl/mqnl_24.png",
						"/static/mqnl/mqnl_25.png",
					]
				],
				emojijugelist:[
					
						[
						"[mnk_早上花]",
						"[mnk_下午花]",
						"[mnk_晚安喵]",
						"[mnk_问号]",
						"[mnk_嘻嘻喵]",
						"[mnk_mua]",
						"[mnk_不吃三吨]",
						"[mnk_好耶1]",
						"[mnk_溜了]",
						"[mnk_美梦]",
						"[mnk_喵]",
						"[mnk_撬棍]",
						"[mnk_嘻嘻]",
						"[mnk_笑嘻了]",
						"[mnk_致命打击]",
						"[mnk_好耶2]",
						"[mnk_+3]",
						"[mnk_+100]",
						"[mnk_DAY0]",
						"[mnk_爱的力量]",
						"[mnk_发点能回的]",
						"[mnk_复读机]",
						"[mnk_姑奶喵]",
						"[mnk_尼奥喵]",
						"[mnk_思考考]",
						"[mnk_小趴菜]",
						"[mnk_总督1]",
						"[mnk_总督2]",
						"[mnk_mona卡]",
						"[mnk_no喵]",
						"[mnk_呃]",
						"[mnk_哼]",
						"[mnk_rua头]",
						"[mnk_上勾拳]",
						"[mnk_手摇奶茶]",
						"[mnk_呜呜喵]",
						"[mnk_雌小鬼]",
						"[mnk_主人主人]",
						],
						[
						"[mnk_mnk]",
						"[mnk_噔噔咚]",
						"[mnk_来了来了]",
						"[mnk_流鼻血]",
						"[mnk_嗯了]",
						"[mnk_你好]",
						"[mnk_菩萨包邮]",
						"[mnk_请]",
						"[mnk_停止响应]",
						"[mnk_再来一局]",
						],
						[
						"[taffy_散步]","[taffy_主人]","[taffy_耶咿]","[taffy_呜呜呜]","[taffy_晚上花]","[taffy_投降]","[taffy_收收味]","[taffy_切割]","[taffy_嗯打游戏]","[taffy_K48]","[taffy_好听]","[taffy_珍珠奶茶灌我嘴里]","[taffy_回私信]","[taffy_活下去]","[taffy_加油喵]","[taffy_好似喵]","[taffy_留条命]","[taffy_啊啊]"
						,"[taffy_绿豆嫌弃]","[taffy_嗯]","[taffy_857]","[taffy_mua喵]","[taffy_白白喵]","[taffy_爆金币咯]","[taffy_别急]","[taffy_不敢想了]","[taffy_不玩了]","[taffy_草喵]","[taffy_超塔菲]","[taffy_吹爆]","[taffy_大骗子]","[taffy_疑惑]","[taffy_单推塔菲]","[taffy_愤怒愤怒!]","[taffy_高伤害]"
						],
						[
							"[明前奶绿_在吗]","[明前奶绿_?]","[明前奶绿_fa店]","[明前奶绿_MA]","[明前奶绿_抱歉]",
							"[明前奶绿_别急]","[明前奶绿_呃呃]","[明前奶绿_放弃]","[明前奶绿_嘿嘿]","[明前奶绿_哼哼]",
							"[明前奶绿_花花]","[明前奶绿_灰头土脸]","[明前奶绿_加油]","[明前奶绿_惊讶]","[明前奶绿_懒]",
							"[明前奶绿_嗯嗯]","[明前奶绿_起床]","[明前奶绿_亲亲]","[明前奶绿_确实]","[明前奶绿_生气]",
							"[明前奶绿_我会了]","[明前奶绿_蟹蟹!]","[明前奶绿_早安]","[明前奶绿_这是什么]","[明前奶绿_真的假的?]",
						]
					
				],
				height2:0,
				show4:0,
				position:"",
				biaoqing:false,
				key:"",
				imageclick:0,
				icon:"../../static/icon.png",
				chooseimage:false,
				backgroundimage:"",
				attentionlist:[],
				chooseimagecolor:"#c4c6c9",
				userheadimage:"",
				myuserheadimage:"",
				myusername:"",
				replydata:"",
				ycsrc:"",
				show:false,
				op:0.95,
				op2:0,
				reply:"",
				replys:[],
				article:"",
				autofocus:false,
				color:"white",
				color1:"#909399",
				username:"",
				title:"",
				tags:[],
				themeid:0,
				show1:false,
				show3:false,
				userid:0,
				jing:0,
				loucengreplyat:{
					userid:0,
					username:"",
					data:""
				},
				status:"loading",
				type:0,
				fangdou:1,
				look:0,
				saveshow:0,
				likecolor:"#ff007f",
				top:0,
				like:0,
				scroll_top:0,
				scroll_top1:"",
				createtime:0,
				username1:"",
				textarea1:18,
				userheadimage1:"",
				mylike:[],
				num:0,
				sign:"",
				height1:0,
				uploadimages:[
					
				],
				replynum:0,
				admin:0,
				savelist:[],
				item:[],
				setWidth:0,
				replytype:1,
				shenfen:"",
				replyslength:0,
				lal:"",
				jugelogin1:false,
				list:[
					{
						type: 'success',
						title: '成功',
						message: "删除成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png',
						url:"index"
					},
					{
						type: 'error',
						title: "失败",
						message:"删除失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'success',
						title: "成功",
						message:"设置成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"设置失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"其它设备登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"请登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'success',
						title: "成功",
						message:"回复成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"回复失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"删除失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'success',
						title: "成功",
						message:"删除成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"内容不能为空",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'error',
						title: "失败",
						message:"账号禁用中",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},

				],
				setWidth:0,
				activity:0,
				setWidth1:0,
				show2:true,
				fangdou1:false,
				getmore:0,
				loadover:0,
				pianyi:{},
				headborder:"",
				keyborde:0,
				
			}
		},
		onBackPress(){
			if(this.imageclick==1){
				this.imageclick=0;
				return true;
			}
			if(this.height2!=0){
				this.height2=0;
				return true;
			}
			if(this.height3!=0){
				this.height3=0;
				return true;
			}
			if(this.show3==1){
				this.show3=0;
				this.setloucengreplyat({
					'userid':0,'data':'','id':0,'username':''
				});
				this.autofocus=false;
				return true;
			}
			
			
		},
		onPageScroll(e) {
			// e.scrollTop 获取页面的滚动高度
			if(e.scrollTop>100)
				this.op2=1;
			else this.op2=0;
		},
		onShow() {
			
	if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=this.color;
			}
			this.userbackgroundimage=getApp().globalData.userbackgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			//console.log(this.userbackgroundimage);
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
							...this.list[4],
							complete() {
								that.loginout();
							}
						})
					}
				}
			})
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					////console.log("admin:"+getApp().globalData.admin);
					this.op=res.data;
				}
			 });
			this.op=getApp().globalData.op;
		},
		methods: {
			test4(){
				this.autofocus=false;
				let _this=this;
				setTimeout(()=>{
					_this.autofocus=true
					
				},50);
			
				
			},
			changeemojiselect(e){
				this.emojiselect=e.detail.current;
			
			},
			addemoji(e,i){
				if(i==0)
				this.reply+=this.emojijugelist[this.emojiselect][e];
				if(i==1)this.replydata+=this.emojijugelist[this.emojiselect][e];
			},
			setloucengreplyat(e){
				
				if(e.userid==getApp().globalData.userid) return;
				this.loucengreplyat.data=e.data;
				this.loucengreplyat.userid=e.userid;
				this.loucengreplyat.id=e.id;
				this.loucengreplyat.username=e.username;
			},
			setactivity(){
				uni.request({
					url:getApp().globalData.http+"/api/setactivity",
					method:"POST",
					data:{
						themeid:this.themeid,
						fenlei:this.fenlei
					},
					success: (res) => {
						if(res.data.code==1001)
							this.activity=1;
					}
				})
			},
			deletefocus(){
				let that=this;
				this.autofocus=false;
				uni.$u.throttle(this.test1, 100,false);
			},
			test1(){
				this.setloucengreplyat({
					'userid':0,'data':'','id':0,'username':''
				});
			},
			deleteactivity(){
				uni.request({
					url:getApp().globalData.http+"/api/deleteactivity",
					method:"POST",
					data:{
						themeid:this.themeid
					},
					success: (res) => {
						if(res.data.code==1001)
							this.activity=0;
					}
				})
			},
			scroll1(e){
				if(e.detail.scrollTop>50)this.op2=1;
				else this.op2=0;
			},
			
			focuss(){
				let _this=this;
			
			},
			tohuifu(){
				uni.navigateTo({
					url:"/pages/index/reply?themeid="+this.themeid
				})
			},
			getreply:function(e){
			
				this.replytype=e;
				this.status="loading";
				uni.request({
					url:getApp().globalData.http+"/api/getreply",
					method:"POST",
					data:{
						"themeid":this.themeid,
						"id":1,
						"replytype":this.replytype
					},
					success: (res) => {
						//console.log(res.data);
						if(res.data.code==1001){
							this.replys=res.data.data;			
							if(res.data.data.length==0){
													
								this.status="nomore";
							}
							else if(res.data.data.length>0&&res.data.data.length<10){
								this.replys[this.replys.length-1].id=this.replys[this.replys.length-1].id+1;
								this.status="nomore";
							}
							else {
								this.getmore=1;
								this.status="loadmore"
							}
						}
						this.fangdou1=false;
					},fail: (res) => {
						this.fangdou1=false;
					}
				})
			},
			getmorereply:function(){
				
				if(this.fangdou1==true&&this.loadover==0)return;this.fangdou1==true;
				var id=0;
				if(this.replys.length==0)id=0;else id=this.replys[this.replys.length-1].id;
				this.status="loading";
				uni.request({
					url:getApp().globalData.http+"/api/getreply",
					method:"POST",
					data:{
						"themeid":this.themeid,
						"id":id,
						"replytype":this.replytype
					},
					success: (res) => {
						//console.log(res.data);
						if(res.data.code==1001){
							for(var i=0;i<res.data.data.length;i++){
								this.replys.push(res.data.data[i]);
							}
							if(res.data.data.length==0){
						
								this.status="nomore";
							}
							else if(res.data.data.length>0&&res.data.data.length<10){
								this.replys[this.replys.length-1].id=this.replys[this.replys.length-1].id+1;
								this.status="nomore";
							}
							else {
								this.getmore=1;
								this.status="loadmore"
							}
						}
						this.fangdou1=false;
					},fail: (res) => {
						this.fangdou1=false;
					}
				})
			},
			test3:function(){
				this.show3=false;
				setTimeout(()=>{this.show3=false},1)
			},
			test2:function(e){
				if(e.atid!=null&&e.atid!=undefined&&e.atid!=0)
				return e.username+": 回复 "+e.atusername+":"+e.data;
				return e.username+":"+e.data;
			},
			deletereplylouceng:function(e){
				uni.request({
					url:getApp().globalData.http+"/api/deleteloucengreply",
					method:"POST",
					data:{
						id:e
					},
					success: (res) => {
						if(res.data.code==1001){
							for(var i=0;i<this.item.loucengreply.length;i++){
								if(this.item.loucengreply[i].id==e){
									this.item.loucengreply.splice(i,1)
									break;
								}
							}
							uni.showToast({
								title:"删除成功",
								icon:"success"
							})
						}else{
							uni.showToast({
								title:"删除失败",
								icon:"error"
							})
						}
					},
					fail:(res)=>{
						uni.showToast({
							title:"删除失败",
							icon:"error"
						})
					}
				})
			},
			replylouceng:function(){
			
				if(this.replydata=="")return;
				uni.request({
					url:getApp().globalData.http+"/api/newloucengreply",
					method:"POST",
					data:{
						userid:getApp().globalData.userid,
						themeid:this.themeid,
						louceng:this.item.louceng,
						data:this.replydata,
						atid:this.loucengreplyat.id,
						atuserid:this.loucengreplyat.userid,
						atusername:this.loucengreplyat.username
					},
					success: (res) => {
						if(res.data.code==1001){
							this.loucengreplyat={
								userid:0,
								id:0,
								data:""
							}
							var temp={
								"username":getApp().globalData.username,
								"userheadimage":getApp().globalData.userheadimage,
								"userid":getApp().globalData.userid,
								"data":this.replydata,
								"time":res.data.time,
								"sign":getApp().globalData.sign,
								"shenfen":res.data.shenfen,
								"id":res.data.id
							}
							for(var i=0;i<this.replys.length;i++){
								if(this.replys[i].louceng==this.item.louceng){
									this.replys[i].loucengreply.push(temp);
									this.replys[i].loucengreplydata='';
									break;
								}
							}
							this.replydata="";
							uni.showToast({
								title:"回复成功",
								icon:"success"
							})
						}else{
							uni.showToast({
								title:"回复失败",
								icon:"error"
							})
						}
					},
					fail:(res)=>{
						uni.showToast({
							title:"回复失败",
							icon:"error"
						})
					}
				})
			},
			test:function(e){
				this.item=e;
				this.show3=true;
			},
			scroll:function(e){
			},
			jugemyself:function(){
				if(this.userid==getApp().globalData.userid)return false;return true;
			},
			addattention:function(){
				uni.request({
					url:getApp().globalData.http+"/api/addattention",
					method:"POST",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"b":this.userid
					},
					success:(res)=>{
						if(res.data.code==1001){
							getApp().globalData.attention.push(this.userid);
							this.attentionlist=getApp().globalData.attention;
						}
					}
				})
			},
			deleteattention:function(){
				uni.request({
					url:getApp().globalData.http+"/api/deleteattention",
					method:"POST",
					data:{
						"a":getApp().globalData.userid,
						"cookie":getApp().globalData.cookie,
						"b":this.userid
					},
					success:(res)=>{
						if(res.data.code==1001){
							for(var i=0;i<getApp().globalData.attention.length;i++){
								if(getApp().globalData.attention[i]==this.userid){
									getApp().globalData.attention.splice(i,1);
									this.attentionlist=getApp().globalData.attention;
								}
							}
						}
					}
				})
			},
			jugeattention:function(){
				this.attentionlist=getApp().globalData.attention;
				for(var i=0;i<this.attentionlist.length;i++){
					if(this.userid==this.attentionlist[i])
						return true;
				}
				return false;
			},
			yulan:function(e){
				uni.previewImage({
							url: e,
							longPressActions: {
								itemList: [],
								success: function(data) {
									
								},
								fail: function(err) {
									
								}
							}
				});
			},
			jugelogin:function(){
				if(getApp().globalData.cookie!='')return true;return false;
			},
			linktag:function(e){
				uni.navigateTo({
					url:"./tag?tagname="+e
				})
			},
			saveadd:function(){
				if(getApp().globalData.cookie==''){
					this.$refs.uToast.show({
						...this.list[5],
						complete() {
							return;
						}
					})
					return;
				}
				uni.request({
					url:getApp().globalData.http+"/api/addsave",
					method:"POST",
					data:{
						"themeid":this.themeid,
						"userid":getApp().globalData.userid
					},
					success: (res) => {
						//console.log(res.data.code);
						if(res.data.code==1001){
							this.saveshow=1;
						}
						
					}
				})
			},
			jugeemoji(e){
				if(e==undefined||e==null)return "";
				for(var j=0;j<this.emojijugelist.length;j++)
				for(var i=0;i<this.emojijugelist[j].length;i++){
					var sub=e.indexOf(this.emojijugelist[j][i]);
					while(sub!=-1){
						var imagename=this.emojilist[j][i];
						imagename="<img src='"+imagename+"' style='width:13vw;height:13vw;margin-left:5px;margin-right:5px'/>";
						e=e.substring(0,sub)
						+imagename+
						e.substring(sub+this.emojijugelist[j][i].length,e.length);
						sub=e.indexOf(this.emojijugelist[j][i]);
					}
				}
				
				return e;
			},
			weizhi(){
				var latitude=this.lal.split(";")[0];
				var longitude=this.lal.split(";")[1];
				console.log(latitude+" "+longitude);
				uni.openLocation({
					latitude: parseFloat(latitude),
					longitude: parseFloat(longitude),
				});
			},
			savedelete:function(){
				uni.request({
					url:getApp().globalData.http+"/api/savedelete",
					method:"POST",
					data:{
						"themeid":this.themeid,
						"userid":getApp().globalData.userid,
					},
					success: (res) => {
						//console.log(res.data.code);
						if(res.data.code==1001){
							this.saveshow=0;
						}
					}
				})
			},
			deletereply:function(e){
				if(!this.jugeuserid(e.userid)){
					return false;
				}
				this.deletelouceng=parseInt(e.louceng);
				this.show1=true;
			},
			deletereply1:function(e){
				let themeid=this.themeid;
				let that=this;
				uni.request({
					url:getApp().globalData.http+"/api/deletereply",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"louceng":this.deletelouceng,
						"themeid":this.themeid
					},
					success: (res) => {
						if(res.data.code==1001){
							
						this.$refs.uToast.show({
							...this.list[9],
							complete() {
								for(var i=0;i<that.replys.length;i++){
									if(that.replys[i].louceng==that.deletelouceng){
										that.replys.splice(i,1);
									}
								}
							}
						})
						}
						else{
							this.$refs.uToast.show({
								...this.list[8],
								complete() {
								
								}
							})
						}
						this.show1=false;
					},
					fail:(res)=>{
						this.$refs.uToast.show({
							...this.list[8],
							complete() {
							
							}
						})
						this.show1=false;
					}
				})
			},
			jugeuserid:function(e){
				if(e==getApp().globalData.userid||getApp().globalData.admin==1)return true;
				return false;
			},
			zuozhe:function(e){
				//console.log(e+" "+this.userid);
				if(e==this.userid)return true;
				return false;
			},
			search:function(){
			
			},
			imagesrc:function(e){
				if(e==null)return;
				
				var arr=e.split(';');
				arr.pop();
				return  arr;
			},
			jugelogin:function(){
				if(getApp().globalData.cookie=="")return false;return true;
			},
			huifu:function(e){
				this.show4=0;
				let themeid=this.themeid;
				let that=this;
				if(this.reply.length==0&&this.uploadimages.length==0){
					that.$refs.uToast.show({
						...this.list[10],
						complete() {
						
						}
					})
					return;
				}
				var image="";
				for(var i=0;i<this.uploadimages.length;i++){
					image=image+this.uploadimages[i]+";";
				}
				this.height2=0;
				uni.request({
					url:getApp().globalData.http+"/api/reply",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"data":this.reply,
						"image":image,
						"themeid":this.themeid,
						"type":e
					},
					success: (res) => {
						
						if(res.data.code==1001){
							this.reply="";
							this.imageclick=0;
							this.uploadimages=[];
							that.$refs.uToast.show({
								...this.list[6],
								complete() {
								
								}
							})
						}
						else if(res.data.code==1002){
							that.$refs.uToast.show({
								...this.list[11],
								complete() {
								}
							})
						}
						else{
							that.$refs.uToast.show({
								...this.list[7],
								complete() {
								}
							})
						}
					},
					fail:(res)=>{
						that.$refs.uToast.show({
							...this.list[7],
							complete() {
							}
						})
					}
				});
			},
			changenum:function(e){
				this.replynum=e.detail.value.length;
			},

			heself1(e){
				uni.navigateTo({
					url:"/pages/index/heself?userid="+e
				})
			},
			changeimagecolor:function(){
				if(this.chooseimagecolor=="#c4c6c9"||this.uploadimages.length>0)
					this.chooseimagecolor="#3c9cff";
				else this.chooseimagecolor="#c4c6c9";
			},
			deleteimage:function(e){
				this.uploadimages.splice(e,1);
				if(this.uploadimages.length==0)this.imageclick=0;
			},
			uploadimage:function(){
				let that=this;
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
								that.uploadimages.push((JSON.parse(res.data)).location);
							}
						})
					}
				});
			},
			linkmyself:function(){
				
			},
			time:function(e){
				var g = new Date().getTime()/1000;
				var time=parseInt(g)-parseInt(e);
				if(time<60)
					return "发布于"+parseInt(time)+"秒前";
				else if(time>=60&&time<60*60)
					return "发布于"+parseInt(time/60)+"分钟前";
				else if(time>=60*60&&time<60*60*24)
					return "发布于"+parseInt(time/60/60)+"小时前"
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
			time1:function(e){
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
			setjing:function(){
				if(this.fangdou!=1)return;
				this.fangdou=0;
				uni.request({
					url:getApp().globalData.http+"/api/setjing",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"themeid":this.themeid
					},
					success: (res) => {
						if(res.data.code==1001){
						this.jing=1;
						this.$refs.uToast.show({
							...this.list[2],
							complete() {
								this.jing=1;
							}
						})}
						else if(res.data.code==1003)
						this.$refs.uToast.show({
							...this.list[4],
							complete() {
							}
						})
						else
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					},
					fail: () => {
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					}
				})
				this.fangdou=1;
			},
			deletejing:function(){
				if(this.fangdou!=1)return;
				this.fangdou=0;
				uni.request({
					url:getApp().globalData.http+"/api/deletejing",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"themeid":this.themeid
					},
					success: (res) => {
						if(res.data.code==1001){
							this.jing=0;
						this.$refs.uToast.show({
							...this.list[2],
							complete() {
								this.jing=0;
							}
						})}
						else if(res.data.code==1003)
						this.$refs.uToast.show({
							...this.list[4],
							complete() {
							}
						})
						else
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					},
					fail: () => {
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					}
				})
				this.fangdou=1;
		},
		

		
		settop:function(){
			if(this.fangdou!=1)return;
			this.fangdou=0;
			uni.request({
				url:getApp().globalData.http+"/api/settop",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie,
					"userid":getApp().globalData.userid,
					"themeid":this.themeid
				},
				success: (res) => {
					if(res.data.code==1001){
						this.top=1;
					this.$refs.uToast.show({
						...this.list[2],
						complete() {
							this.top=1;
						}
					})
					}
					else if(res.data.code==1003)
					this.$refs.uToast.show({
						...this.list[4],
						complete() {
						}
					})
					else
					this.$refs.uToast.show({
						...this.list[3],
						complete() {
						}
					})
				},
				fail: () => {
					this.$refs.uToast.show({
						...this.list[3],
						complete() {
						}
					})
				}
			})	
			this.fangdou=1;
		},
			deletetop:function(){
				if(this.fangdou!=1)return;
				this.fangdou=0;
				uni.request({
					url:getApp().globalData.http+"/api/deletetop",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie,
						"userid":getApp().globalData.userid,
						"themeid":this.themeid
					},
					success: (res) => {
						if(res.data.code==1001){
							this.top=0;
						this.$refs.uToast.show({
							...this.list[2],
							complete() {
								this.top=0;
							}
						})}
						else if(res.data.code==1003)
						this.$refs.uToast.show({
							...this.list[4],
							complete() {
							}
						});
						else
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					},
					fail: () => {
						this.$refs.uToast.show({
							...this.list[3],
							complete() {
							}
						})
					}
				})
				this.fangdou=1;
			},
			changeop:function(){
				getApp().globalData.op=this.op;
				uni.setStorage({
				    key: "op",
				    data: getApp().globalData.op,
				    success: function () {
				    }
				});
			},
			find:function(){
				
			},
			linkto:function(){
				uni.navigateTo({
					url:"outpage?url="+this.ycsrc
				})
			},
			showToast(params) {
				this.$refs.uToast.show({
					...params,
					complete() {
					params.url && uni.navigateTo({
						url: params.url
					})
					}
				})
			},
			delete_theme:function(){
				this.show=false;
				uni.request({
					url:getApp().globalData.http+"/api/deletetheme",
					method:"POST",
					data:{
						"themeid":this.themeid
					},
					success: (res) => {
						this.showToast(this.list[0]);
					},
					fail: (res) => {
						this.showToast(this.list[1]);
					}
				})
			},
			heself:function(e){
				if(e==1){
					if(this.op2==0)return;
				}
				
				uni.navigateTo({
					url:"heself?userid="+this.userid
				})
			},
			heself1:function(e){
			uni.navigateTo({
				url:"heself?userid="+e
			})
			},
			back:function(){
				uni.navigateBack({
					delta:1
				})
			},
			setlike:function(e){
				if(getApp().globalData.cookie==''){
					this.$refs.uToast.show({
						...this.list[5],
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
							this.like=this.like+1;
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
									this.like=this.like-1;
									break;
								}
							}
							
						}
					}
				})
			},
			jugelike:function(res){

				for(var i=0;i<this.mylike.length;i++){
					if(this.mylike[i]==parseInt(res))return true;
				};return false
			},
			juge(){
				////console.log(getApp().globalData.userid==this.userid);
				if(getApp().globalData.userid==this.userid||getApp().globalData.admin==1)return true;else return false;
			},
			juge_admin(){
				if(getApp().globalData.admin==1)
					return true;
				else return false;
			},
			
		},
		onLoad(res) {
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
			let _this=this
			uni.getSystemInfo({
				success: function (res){
				_this.setWidth = res.windowWidth * 0.6;
				_this.setWidth1 = res.windowWidth * 0.25
				}
			
			})
			this.myuserheadimage=getApp().globalData.userheadimage
			let that=this;
			uni.onKeyboardHeightChange(res => {
			  that.keyborde=res.height
			  if(res.height>0){
				  that.textarea1=54;
			  }else that.textarea1=18;
			})
			this.myusername=getApp().globalData.username;
			this.backgroundimage=getApp().globalData.backgroundimage;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			this.op=getApp().globalData.op;
			this.themeid=parseInt(res.themeid);
			let id2=res.id;
			if(getApp().globalData.cookie!=''){
				this.jugelogin1=true;
			}
			if(getApp().globalData.cookie!='')
			uni.request({
				url:getApp().globalData.http+"/api/getmyattention",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie,
					"userid":getApp().globalData.userid
				},
				success: (res) => {
					if(res.data.code==1001){
						getApp().globalData.attention=res.data.data;
			
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
							getApp().globalData.mylike=res.data.mylike;
							this.mylike=res.data.mylike;
							
						}
					}
				})
			}
			uni.request({
				url:getApp().globalData.http+"/api/getmysave",
				method:"POST",
				data:{
					"userid":getApp().globalData.userid
				},
				success: (res) => {
					this.savelist=res.data;
					for(var i=0;i<res.data.length;i++){
						if(this.themeid==res.data[i]){
							this.saveshow=1;
							break;
						}
					}
					
				}
			})
			var id1=1;
			if(res.id!=null)id1=res.id;
			this.status="loading";
			uni.request({
				url:getApp().globalData.http+"/api/getreply",
				method:"POST",
				data:{
					"themeid":this.themeid,
					"id":id1,
					"replytype":3
					
				},
				success: (res) => {
					//console.log(res.data);
					this.loadover=1;
					if(res.data.code==1001){
						this.replys=res.data.data;
						if(this.replys.length<10){
							this.status="nomore"
							if(this.replys.length>0)
							this.replys[this.replys.length-1].id=
							this.replys[this.replys.length-1].id+1;
						}else{
							this.status="loadmore"
							this.replys[this.replys.length-1].id=
							this.replys[this.replys.length-1].id+1;
						}
						if(id2!=null){
							setTimeout(() => {  
								that.scroll_top1='a'+id2
							}, 500)
						}
					}
				}
			})
			uni.request({
				url:getApp().globalData.http+"/api/gettheme",
				method:"POST",
				data:{
					"themeid":parseInt(res.themeid)
				},
				success: (res) => {
					
					this.show2=false;
					this.jing=res.data.data.jing;
					this.top=res.data.data.top;
					this.type=res.data.data.type;
					this.ycsrc=res.data.data.ycsrc;
					if(res.data.data.position!=null&&res.data.data.position!=undefined){
						this.position=res.data.data.position;
						this.lal=res.data.data.lal;
					}
					let temp=res.data.data.text.indexOf("style='width:auto;height:auto'");
					while(temp!=-1){
						res.data.data.text=res.data.data.text.substring(0,temp+29)+";margin-top:10px;border-radius:5px'"+res.data.data.text.substring(temp+30,res.data.data.text.length);
						temp=res.data.data.text.indexOf("style='width:auto;height:auto'");
					}
					this.article=res.data.data.text;
					this.title=res.data.data.title;
					this.replyslength=res.data.data.num;
					if(this.title!='')
					uni.setNavigationBarTitle({
							title:this.title
					})
					else
					uni.setNavigationBarTitle({
							title:"主题"
					})
					
					this.tags=res.data.data.tags.split(";");
					this.tags.pop();
					this.activity=res.data.data.activity;
					this.userid=res.data.data.userid;
					this.fenlei=res.data.data.fenlei
					this.username1=res.data.data.username;
					this.look=res.data.data.look;
					this.userheadimage1=res.data.data.userheadimage;
					this.headborder=res.data.data.headborder;
					this.pianyi=res.data.data.pianyi;
					this.createtime=res.data.data.createtime;
					this.like=res.data.data.likes;
					this.num=res.data.data.num;
					this.sign=res.data.data.sign;
					this.admin=res.data.data.admin;
					this.shenfen=res.data.data.shenfen;
					////console.log(this.article);
					var jugehistory=0;
					var history={
						"title":this.title,
						"data":res.data.data.data,
						"themeid":this.themeid,
						"time":new Date().getTime()
					}
					for(var i=0;i<getApp().globalData.history.length;i++){
						if(getApp().globalData.history[i].themeid==this.themeid){
							getApp().globalData.history[i].time=new Date().getTime();
							jugehistory=1;
						}
					}
					if(jugehistory==0)getApp().globalData.history.unshift(history);
					uni.setStorage({
					    key: "history",
					    data: getApp().globalData.history,
					    success: function () {
					    }
					});
				}
			})
		}
		
	}
</script>

<style>
.op{
	opacity: 0.95; 
}
.mp{
	user-select:text;
}
.textarea1{
	height:100px
}
.bottom1{
	margin-bottom:10vh
}
.bottom2{
	margin-bottom:5vh
}
.s1{
	padding-bottom: 1vh;
}
.s2{
	margin-bottom: 1vh;
}
.selectemoji{
	background-color: #f6f7f8;
}
</style>
