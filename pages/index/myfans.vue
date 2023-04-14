<template>
	<view style="height:95.6vh;width:100vw">
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
				 style="font-weight: 700;">我的粉丝</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:0px">
			1
		</view>
		<scroll-view style="height: 100%;" scroll-y @scrolltolower="getmorefans()">
		<view v-for="(item,index) in fanss"  style="padding-bottom:10px;border-bottom: 0.5px solid #dee2eb;margin-left: 5px;display: flex;flex-direction: row;margin-bottom: 10px;height:auto;width:94%;margin-left:3%;margin-right:3%;margin-top: 10px;" >
			<view style="margin-right: 5px;" @click="heself(item.userid)">
				<u-avatar :src="item.userheadimage" v-if="item.userheadimage!=''"></u-avatar>
				<u-avatar :text="sb(item.username)" v-if="item.userheadimage==''"></u-avatar>
			</view>
			<view style="margin-left: 5px;display: flex;flex-direction: column;height:40px;justify-content: center;" @click="heself(item.userid)">
				<text>{{item.username}}</text>
			
			</view>
			<view style="margin-top: 5px;width:50px;height:30px;background-color: #3c9cff;border-radius: 3px;display: flex;align-items: center;justify-content: center;color:white;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="!jugeattention(item.userid)" @click="addattention(item.userid)">关注</view>
			<view style="margin-top: 5px;width:50px;height:30px;background-color: #ecf5ff;border: 0px solid #3c9cff;color:#3c9cff;display: flex;align-items: center;justify-content: center;border-radius: 3px;font-size: 15px;margin-left: auto;margin-right: 10px;"  v-show="jugeattention(item.userid)" @click="deleteattention(item.userid)">已关注</view>
		</view>
		<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;margin-bottom: 10px;margin-top:10px;font-size:14px;color:#787878" >
			<text>没有更多了</text>
		</view>
							</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fansfangdou:0,
				fanspage:0,
				fanss:[],
				attentionlist:[],
				color:"white",
				color1:"black",
			}
		},
		onLoad(){
			if(getApp().globalData.skinchoose!=0){
				this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
				this.color1=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
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
		methods: {
			back(){
				uni.navigateBack();
			},
			heself:function(e){
				uni.navigateTo({
					url:"heself?userid="+e
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
			sb(e){
				var str='';str+=e;
				return str.substr(0,1);
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
			jugetouxiang:function(e){
				var touxiang="";
				touxiang=e;
				if(touxiang==undefined){
				return true;
				}
			
				return false;
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
		}
	}
</script>

<style>

</style>
