<template>
	<view style="width: 100vw;height:100%;background-size: cover;background-attachment: fixed;background-color: white;">

		<!--*************************-->
		<view style="display: flex;flex-direction: row;display: flex;justify-content: center;">
			<view style="background-size:100vw auto;width:95vw;height:9vh;padding-left:2.5vw;padding-right: 2.5vw;"
				:style="{backgroundColor:color2,backgroundImage:'url(' + backgroundimage + ')'}"
			>
				<view style="font-size: 20px;font-weight: 700;padding-top: 4.5vh;margin-bottom:25px;">
					<text :style="{color:color1}">消息</text>
				</view>
				<u-divider v-if="skinchoose==0"></u-divider>
				<view style="height:10px;width:100vw;" v-if="skinchoose!=0">
					
				</view>
				<view style="display: flex;flex-direction: row;margin-top: -10px;">
					<view style="margin-left: 10px;" v-if="choose!=0" @click="choose=0,getmore1()">
						<text>回复我的</text>
					</view>
					<view style="display: flex;flex-direction: column;margin-left: 10px;" v-if="choose==0">
						<text 
						:style="{color:likecolor}"
						>回复我的</text>
						<view
							style=";width:auto;height:2px;border-radius: 1px;margin-top: 5px;"
							:style="{backgroundColor:likecolor}"
							>
						</view>
					</view>
					<view style="margin-left: 30px;" v-if="choose!=1" @click="choose=1,getmy_systemmessage1()">
						<text>系统消息</text>
					</view>
					<view style="display: flex;flex-direction: column;margin-left: 30px;" v-if="choose==1">
						<text 	:style="{color:likecolor}">系统消息</text>
						<view
							style=";width:auto;height:2px;border-radius: 1px;margin-top: 5px;"
							:style="{backgroundColor:likecolor}"
							>
						</view>
					</view>
					<view style="margin-left: 30px;" v-if="choose!=2" @click="choose=2,getmychat()">
						<text>私信</text>
					</view>
					<view style="display: flex;flex-direction: column;margin-left: 30px;" v-if="choose==2">
						<text 	:style="{color:likecolor}">私信</text>
						<view
							style=";width:auto;height:2px;border-radius: 1px;margin-top: 5px;"
							:style="{backgroundColor:likecolor}"
							>
						</view>
					</view>
				</view>
				<scroll-view style="margin-top:20px;height:80vh;background-color: white;width:100%;;" :scroll-y="true"
					@scrolltolower="getmore()" v-if="choose==0">
					<view v-for="(item,index) in themelist" style="margin-bottom: 15px;"
						@click="theme(item.themeid,item.id)">
						<view style="display: flex;flex-direction:row;align-items: center;">
							<userhead style="z-index: 1;;width:40px;height:40px" :size="'40'" :username="item.username"
								:userheadimage="item.userheadimage" :headborder="item.headborder" :pianyi="item.pianyi">
							</userhead>
							<view style="display: flex;flex-direction:column;margin-left:8px">
								<text style="font-size: 16px;">{{item.username}}</text>
								<text style="font-size: 12px;color:#909399;">{{time(item.time)}} 回复了我</text>
							</view>
						</view>
						<view
							style="width:auto;height:auto;background-color:#f4f4f5;margin-top:20px;border-radius:5px;padding:10px;padding-top:10px">
							<u--text v-if="item.type==1" :lines="2" :text=" item.louceng+'楼:'+item.data" size="15">
							</u--text>
							<u--text v-if="item.type==2" :lines="2" :text=" item.data" size="15"></u--text>
							<text>{{image1(item.image)}}</text>
							<view
								style="width:90%;height:auto;background-color:white;border-radius:5px;padding:15px;margin-top:10px;display:flex;flex-direction:row;align-self: center;">
								<view v-if="item.type==1&&item.themeimage!=null&&item.themeimage.length>0"
									style="margin-right: 10px;">
									<image :src="image(item.themeimage)"
										style="width:70px;height:70px;border-radius:5px" mode="aspectFill"></image>
								</view>
								<u--text v-if="item.type==1" :lines="2"
									:text="username+':'+item.title+'\n'+item.themedata+image1(item.themeimage)"
									size="14"></u--text>
								<u--text v-if="item.type==2" :lines="2"
									:text="username+' '+item.louceng+'楼:'+item.title+'\n'+item.themedata+image1(item.themeimage)"
									size="14"></u--text>

							</view>
						</view>
					</view>
					<u-loadmore :status="status" loading-text="努力加载中" loadmore-text="轻轻上拉" nomore-text="实在没有了" />
					<view style="width:100vw;height:5vh;opacity: 0;">
						<text> </text>
					</view>
				</scroll-view>
				<scroll-view style="margin-top:20px;height:80vh;background-color: white;width:100%;;" :scroll-y="true"
					@scrolltolower="getmy_systemmessage" v-if="choose==1">
					<view v-for="(item,index) in systemmessage" style="margin-bottom: 15px;">
						<view style="display: flex;flex-direction:row;align-items: center;">
							<u-avatar mode="aspectFill" :src="item.systemheadimage+'?imageMogr2/thumbnail/300x300'"
								size="40"></u-avatar>

							<view style="display: flex;flex-direction:column;margin-left:5px">
								<text style="font-size: 14px;">{{item.systemname}}</text>
								<text style="font-size: 12px;color:#909399;">{{time(item.createtime)}}</text>
							</view>
						</view>
						<view
							style="width:94vw;height:auto;background-color:#f4f4f5;margin-top:20px;border-radius:5px;padding-left:1vw;padding-right:1vw;padding-bottom: 1vh; padding-top:1vh;margin-right: 1vw;overflow-x: hidden;">
							<u--text :text="item.message" size="15"></u--text>
							<u--text :lines="1" text="地址链接" size="15" color="#3c9cff" style="margin-top: 5px;"
								@click="linkto1(item.src)" v-if="item.src!=''"></u--text>
						</view>
						<u--image :src="item.images+'?imageMogr2/crop/x3000/thumbnail/600000@'"
							style="margin-right:1rem;margin-top: 15px;" width="96vw" radius="5px"
							v-if="item.images!=''"></u--image>
					</view>
					<u-loadmore :status="status" loading-text="努力加载中" loadmore-text="轻轻上拉" nomore-text="实在没有了" />
					<view style="width:100vw;height:5vh;opacity: 0;">
						<text> </text>
					</view>
				</scroll-view>
				<scroll-view style="margin-top:20px;height:80vh;background-color: white;width:100%;;" :scroll-y="true"
					@scrolltolower="getmore()" v-if="choose==2">
					<view v-for="(item,index) in chat" @click="tochat(item)">
						<view style="display: flex;flex-direction:row;align-items: center;width:96vw">
							<u-avatar mode="aspectFill" :src="item.userheadimage+'?imageMogr2/thumbnail/300x300'"
								v-if="item.userheadimage!=null" size="45"></u-avatar>
							<u-avatar :text="item.username.substr(0,1)" randomBgColor v-if="item.userheadimage==null"
								size="45"></u-avatar>
							<view style="display: flex;flex-direction: column;width:90%">
								<view style="display: flex;flex-direction:row;margin-left:8px;align-items: center;">
									<text style="font-size: 16px;">{{item.username}}</text>
									<view style="margin-left:auto;margin-right: 5px;">
										<text style="font-size: 14px;color:#909399;">{{time1(item.time)}} </text>
									</view>
								</view>
								<view style="display: flex;flex-direction:row;margin-left:8px;align-items: center;">
									<u--text :lines="1" color="#898b91" :text="item.message+'[图片]'"
										v-if="item.image.length>0"></u--text>
									<u--text :lines="1" color="#898b91" :text="item.message"
										v-if="item.image.length==0"></u--text>
								</view>
							</view>
						</view>
						<u-divider></u-divider>
					</view>


					<view style="width:100vw;height:5vh;opacity: 0;">
						<text> </text>
					</view>
				</scroll-view>
			</view>
			<!---->
		</view>

	</view>
</template>

<script>
	import userhead from "@/pages/index/userhead/userhead.vue"
	export default {
		components: {
			userhead
		},
		data() {
			return {
				status: "nomore",
				username: "",
				userheadimage: "",
				admin: 0,
				userbackgroundimage: "",
				choose: 2,
				themelist: [],
				juge: 1,
				systemmessage: [],
				likecolor:"#ff007f",
				chat: [],
				limit: 0,
				timer: null,
				fangdou1: 0,
				page: 0,
				color1:"black",
				color:"white",
				color2:"",
				skinchoose:0,
				backgroundimage:"",
			}
		},
		mounted() {
			if(getApp().globalData.skinchoose!=0){
				this.skinchoose=1;
				this.color2=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				this.likecolor=this.color2;
				this.backgroundimage=getApp().globalData.skin[getApp().globalData.skinchoose-1].backgroundimage;
			}
			this.username = getApp().globalData.username;
			this.userheadimage = getApp().globalData.userheadimage;
			this.admin = getApp().globalData.admin;
			this.userbackgroundimage = getApp().globalData.userbackgroundimage;
			this.chat = getApp().globalData.chat;
			this.timer = setInterval(() => {
				this.getmychat(); // 业务逻辑	
			}, 5)
		},
		onShow() {
			getApp().globalData.replymessagenum = 0;
			this.getmychat();
			this.getmore();
		},
		methods: {
			tochat: function(res) {
				var url = "chat?userid=" + res.userid + "&username=" + res.username + "&userheadimage=" + res
					.userheadimage;
				uni.navigateTo({
					url: url
				})
			},
			getmychat() {
				for (var i = 0; i < getApp().globalData.chat.length - 1; i++) {
					//console.log(getApp().globalData.chat[i].time);
				}
				for (var i = 0; i < getApp().globalData.chat.length - 1; i++) {
					for (var j = i + 1; j < getApp().globalData.chat.length; j++)
						if (getApp().globalData.chat[i].time < getApp().globalData.chat[j].time) {
							var temp = getApp().globalData.chat[i];
							getApp().globalData.chat[i] = getApp().globalData.chat[j];
							getApp().globalData.chat[j] = temp;
						}
				}
				this.chat = getApp().globalData.chat;
				for (var j = 0; j < this.chat.length; j++)
					for (var i = getApp().globalData.chatlist.length - 1; i >= 0; i--) {
						if ((getApp().globalData.chatlist[i].a == this.chat[j].userid || getApp().globalData.chatlist[i]
								.b == this.chat[j].userid) &&
							getApp().globalData.chatlist[i].time > 0) {
							this.chat[j].message = getApp().globalData.chatlist[i].message;
							this.chat[j].time = getApp().globalData.chatlist[i].time;
							break;
						}
					}
			},
			getmy_systemmessage1: function() {
				this.status == "loading";
				this.page = 0;
				uni.request({
					url: getApp().globalData.http + "/api/getmy_systemmessage",
					method: "POST",
					data: {
						userid: getApp().globalData.userid,
						cookie: getApp().globalData.cookie,
						page: this.page
					},
					success: (res) => {

						this.systemmessage = res.data;
						if (res.data.length < 5) {
							this.fangdou1 = 1;
							this.page = -1;
							this.status = "nomore";
						} else {
							this.fangdou1 = 0;
							this.page++;
							this.status = "loadmore";
						}
					},
					fail: (res) => {

					},
				})
			},
			getmy_systemmessage: function() {
				if (this.fangdou1 == 1) return;
				this.fangdou1 = 1;
				this.status == "loading";
				uni.request({
					url: getApp().globalData.http + "/api/getmy_systemmessage",
					method: "POST",
					data: {
						userid: getApp().globalData.userid,
						cookie: getApp().globalData.cookie,
						page: this.page
					},
					success: (res) => {
						for (var i = 0; i < res.data.length; i++)
							this.systemmessage.push(res.data[i]);
						if (res.data.length < 5) {
							this.fangdou1 = 1;
							this.page = -1;
							this.status = "nomore";
						} else {
							this.fangdou1 = 0;
							this.page++;
							this.status = "loadmore";
						}
					},
					fail: (res) => {

					},
				})
			},
			choose2: function() {

			},
			linkto1: function(e) {
				uni.navigateTo({
					url: "outpage?url=" + e
				})
			},
			getmore1: function() {
				this.status = "loading";
				this.limit = 0;
				uni.request({
					url: getApp().globalData.http + "/api/getreplymessage",
					method: "POST",
					data: {
						"limit": this.limit,
						"userid": getApp().globalData.userid,
						"cookie": getApp().globalData.cookie
					},
					success: (res) => {
						this.juge = 1;
						console.log(res);
						if (res.data.reply.length == 0 || res.data.reply.length < 10) {
							this.juge = 0;
							this.status = "nomore";

						} else
							this.limit++;

						for (var i = 0; i < res.data.reply.length; i++) {

							//	console.log(res.data.reply[i].data);
							var msg = res.data.reply[i].data;
							while (msg.indexOf("<pre") != -1) {
								var x = msg.indexOf("<pre");
								var y = msg.indexOf("</pre>");
								msg = msg.substring(0, x) + "[代码块]" + msg.substring(y + 6, msg.length);
							}
							var re2 = new RegExp("\n", "g"); //匹配html标签的正则表达式，"g"是搜索匹配多个符合的内容
							msg = msg.replace(re2, ''); //执行替换成空字符
							var re1 = new RegExp("<.+?>", "g"); //匹配html标签的正则表达式，"g"是搜索匹配多个符合的内容
							msg = msg.replace(re1, ''); //执行替换成空字符
							res.data.reply[i].data = msg.toString();
							if(getApp().globalData.replymessage.length==0)
							getApp().globalData.replymessage=[];
							getApp().globalData.replymessage.push(res.data.reply[i]);


						}
						this.themelist = res.data.reply;
					},fail: (res) => {
						console.log(res);
					}
				})
			},
			getmore: function() {
				if (this.juge == 0) return;
				this.juge = 0;
				this.status = "loading";

				uni.request({
					url: getApp().globalData.http + "/api/getreplymessage",
					method: "POST",
					data: {
						"limit": this.limit,
						"userid": getApp().globalData.userid,
						"cookie": getApp().globalData.cookie
					},
					success: (res) => {
						console.log(res);
						this.juge = 1;
						if (res.data.reply.length == 0 || res.data.reply.length < 10) {
							this.juge = 0;
							this.status = "nomore";

						}
						this.limit++;

						for (var i = 0; i < res.data.reply.length; i++) {

							//	console.log(res.data.reply[i].data);
							var msg = res.data.reply[i].data;
							while (msg.indexOf("<pre") != -1) {
								var x = msg.indexOf("<pre");
								var y = msg.indexOf("</pre>");
								msg = msg.substring(0, x) + "[代码块]" + msg.substring(y + 6, msg.length);
							}
							var re2 = new RegExp("\n", "g"); //匹配html标签的正则表达式，"g"是搜索匹配多个符合的内容
							msg = msg.replace(re2, ''); //执行替换成空字符
							var re1 = new RegExp("<.+?>", "g"); //匹配html标签的正则表达式，"g"是搜索匹配多个符合的内容
							msg = msg.replace(re1, ''); //执行替换成空字符
							res.data.reply[i].data = msg.toString();
							getApp().globalData.replymessage.push(res.data.reply[i]);
							this.themelist.push(res.data.reply[i]);

						}
					},fail: (res) => {
						console.log(res);
					}
				})
			},
			theme: function(e, i) {
				uni.navigateTo({
					url: "./theme?themeid=" + e + "&id=" + i
				})
			},
			image1: function(e) {
				if (e == null || e == undefined || e.length == 0) return "";
				var arr = e.split(";")
				arr.pop();
				var str = "";
				for (var i = 0; i < arr.length; i++)
					str += "[图片]";
				return str;
			},
			image: function(e) {
				return e.split(";")[0] + '?imageMogr2/crop/x3000/thumbnail/600000@';
			},
			time: function(e) {
				var g = new Date().getTime() / 1000;
				var time = parseInt(g) - parseInt(e);
				if (time < 60)
					return "" + parseInt(time) + "秒前";
				else if (time >= 60 && time < 60 * 60)
					return "" + parseInt(time / 60) + "分钟前";
				else if (time >= 60 * 60 && time < 60 * 60 * 24)
					return "" + parseInt(time / 60 / 60) + "小时前"
				else {
					var g = new Date().getTime();
					var d = new Date(g);
					var e = new Date(e * 1000);
					var year = d.getFullYear();
					var month = d.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date = d.getDate();
					var year1 = e.getFullYear();
					var month1 = e.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date1 = e.getDate();
					if (year != year1)
						return year1 + "-" + month1 + "-" + date1;
					else return month1 + "-" + date1;
				}
			},
			time1: function(e) {
				var g = new Date();
				var e1 = new Date(e * 1000);
				var data = g.getDate();
				var data1 = e1.getDate();
				if (data == data1) {
					let date = new Date(e * 1000);
					let h = date.getHours();
					let m = date.getMinutes();
					if (m < 10)
						m = "0" + m;
					return h + ":" + m
				} else {
					var g = new Date().getTime();
					var d = new Date(g);
					var e = new Date(e * 1000);
					var year = d.getFullYear();
					var month = d.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date = d.getDate();
					var year1 = e.getFullYear();
					var month1 = e.getMonth() + 1; //取得日期中的月份，其中0表示1月，11表示12月
					var date1 = e.getDate();
					//if(year!=year1)
					return year1 + "-" + month1 + "-" + date1;
					//else return month1+"-"+date1;
				}
			},
		}
	}
</script>

<style>

</style>
