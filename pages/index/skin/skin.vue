<template>
	<view>
		<view style="width:100vw;height:45px;display: flex;flex-direction: row;align-items: center;justify-content: center;padding-top:4.2vh;border-bottom: 1px solid #e6ebf4;margin-bottom: 15px;
		position:fixed;top:0;z-index:2
		"
		:style="{backgroundColor:color}"
		>
			<view style="width:33vw;display: flex;align-items: center;">
				<u-icon
				 :color="fontcolor"
				 name="arrow-left" size="20" style="margin-left: 2vw;" @click="back()"></u-icon>
			</view>
			<view style="width:33vw;display: flex;flex-direction: row;align-items: center;justify-content: center">
				<text
				 :style="{color:fontcolor}"
				 style="font-weight: 700;">主题装扮</text>
			</view>
			<view style="width:33vw">
			
			</view>
		</view>
		<view style="opacity:0;width:100vw;margin-top:4.2vh;height:45px;margin-bottom:15px">
			1
		</view>
		
		<view
		 v-for="(item,index) in skinlist"
		 @click="open1(item.id)"
		 style="width:95vw;margin-left: 2.5vw;height:160px;border-radius: 15px;margin-bottom: 20px;
		 background-repeat:no-repeat;background-size: 96vw 160px;overflow: hidden;box-shadow:#bfc3cb 0px 5px 10px 0px;
		 "
		:style="{backgroundImage:'url(http://49.232.23.79:8081'+item.share+')'}"
		 >
			<view style="width:80%;height:100%;
			background-image:linear-gradient(to right,rgba(255,0,127,1),rgba(255,0,127,0)) ;
			"
			:style="{backgroundImage:item.linear2}"
			>	
				<view style="width:95%;margin-left:2.5%;display: flex;flex-direction: row;align-items: center">
					<image :src="userheadimage" style="margin-right: 10px;margin-top: 20px;width:35px;height:35px;border-radius: 50%;" mode="aspectFit"></image>
					<text style="color:white;font-size: 15px;margin-top: 20px;">{{item.name}}</text>
				</view>
				<view style="width:70%;margin-left: 2.5%;margin-top: 10px">
					<text style="font-size: 12px;color:white;">{{item.tip}}</text>
				</view>
			</view>
		</view>
		
		<view style="box-shadow:#909399 0px 5px 10px 0px;width:95vw;margin-left: 2.5vw;height:150px;border-radius: 15px;margin-bottom: 20px;"
		@click="open1(0)"
		>
			<view style="width:100%;height:100%;border-radius: 15px;
			background-image:linear-gradient(to right,rgba(255,0,127,1),rgba(255,0,127,0)) ;
			">	
				<view style="width:95%;margin-left:2.5%;display: flex;flex-direction: row;align-items: center">
					<image :src="userheadimage" style="margin-right: 10px;margin-top: 20px;width:35px;height:35px;border-radius: 50%;" mode="aspectFit"></image>
					<text style="color:white;font-size: 15px;margin-top: 20px;">默认主题</text>
				</view>
				<view style="width:95%;margin-left: 2.5%;margin-top: 10px">
					<text style="font-size: 12px;color:white;">学伴 WMU</text>
				</view>
			</view>
		</view>
		
		<view >
			<u-modal :show="show" title="切换主题" :content='"是否切换主题为"+tips' :closeOnClickOverlay="true" @cancel="show=false,fangdou=0" :showCancelButton="true" @close="show=false" @confirm="changeskin"></u-modal>
		</view>
		
		<u-popup :show="show1" >
		    <view style="width:100vw;height:100px;background-color: rgba(255,255,255,0);
			display: flex;flex-direction: column;align-items: center;justify-content: center
			">
		        <view style="padding-left: 10vw;;width:80vw;margin-right:10vw;height:80px;background-color: white;border-radius:15px;text-align: center;;display: flex;flex-direction: column;align-items: center;justify-content: center ">
					<u--text :text="tips+' 下载中'" align="center"></u--text>
					<view style="width:100%;margin-top: 10px;">
					<u-line-progress :percentage="parseFloat(downloadnow/downloadnum*100).toFixed(2)" activeColor="#3c9cff"></u-line-progress>
					</view>
				</view>
		    </view>
		</u-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				skinid:0,
				skinlist:[],
				color:"white",
				fontcolor:"black",
				userheadimage:"",
				show:false,
				tips:"",
				tempid:0,
				downloadnum:0,
				downloadnow:0,
				bottomtar:[
				{
					image1:"",
					image2:"",
				},
				{
					image1:"",
					image2:"",
				},
				{
					image1:"",
					image2:"",
				},
				{
					image1:"",
					image2:"",
				},],
				bottomtarstr:"",
				backvideostr:"",
				backvideo:[],
				backgroundimage:"",
				starimage:"",
				newthemeicon:"",
				button:"",
				share:"",
				fangdou:0,
				show1:false,
			}
		},
		onLoad(){
			uni.request({
				url:getApp().globalData.http+"/api/getskinlist",
				method:"POST",
				data:{},
				success: (res) => {
					this.skinlist=res.data;
					for(var i=0;i<this.skinlist.length;i++){
						for(var j=0;j<getApp().globalData.skin.length;j++){
							if(getApp().globalData[j].id==this.skinlist[i].id){
								this.skinlist[i].share=getApp().globalData.skin[j].share;
								break;
							}
						}
					}
				}
			})
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
			this.open();
		},
		methods: {
			
			open1(e){
				if(this.fangdou==1)return;
				this.fangdou=1;
				if(e==0)this.tips="默认主题";else this.tips=this.skinlist[e-1].name;
				this.tempid=e;
				this.show=true;
			},
			juge(){
				if(this.downloadnum==this.downloadnow){
					
					let usesvga1=true;
					if(this.skinlist[this.tempid-1].usesvga==0)usesvga1=false;
					var temp={
						id:this.tempid,
						backgroundnum:this.skinlist[this.tempid-1].backgroundnum,
						choosebackground:0,
						name:this.skinlist[this.tempid-1].name,
						tip1:this.skinlist[this.tempid-1].tip1,
						tip:this.skinlist[this.tempid-1].tip,
						starimage:this.starimage,
						backgroundimage:this.backgroundimage,
						backvideo:this.backvideo,
						share:this.share,
						skincolor:this.skinlist[this.tempid-1].skincolor ,
						tabcolor:this.skinlist[this.tempid-1].tabcolor,
						tabcolor1:"#b90000",
						tabcolor2:"#68615c",
						selectcolor:this.skinlist[this.tempid-1].selectcolor,
						unselectcolor:this.skinlist[this.tempid-1].unselectcolor,
						linear:this.skinlist[this.tempid-1].linear,
						linear1:this.skinlist[this.tempid-1].linear1,
						linear2:this.skinlist[this.tempid-1].linear2,
						button:this.button,
						newthemeicon:this.newthemeicon,
						usesvga:usesvga1,
						bottomtar:this.bottomtar
					}
				if(getApp().globalData.skin.length<this.tempid){
					for(var i=getApp().globalData.skin.length;i<this.tempid;i++){
						getApp().globalData.skin.push({});
					}
				}
				getApp().globalData.skin[this.tempid-1]=temp;
				uni.setStorage({
					key: "skin",
					data: getApp().globalData.skin,
					success: function () {
					}
				});
				getApp().globalData.skinchoose=this.tempid;
				uni.setStorage({
					key: "skinchoose",
					data: getApp().globalData.skinchoose,
					success: function () {
					}
				});
				this.show1=false;
				plus.runtime.restart();
			}
			},
			changeskin(){
				this.show=false;
				this.show1=true;
				
				if(this.tempid==0){
					uni.setStorage({
						key: "skinchoose",
						data: 0,
						success: function () {
						}
					});
					plus.runtime.restart();
					return;
				}
				for(let i=0;i<getApp().globalData.skin.length;i++){
					if(undefined!=getApp().globalData.skin[i].id&&this.tempid==getApp().globalData.skin[i].id){
						uni.setStorage({
							key: "skinchoose",
							data: this.tempid,
							success: function () {
							}
						});
						plus.runtime.restart();
						return;
					}
				}
				let that=this;
				this.backvideostr=this.skinlist[this.tempid-1].backvideo.split(";");
				this.bottomtarstr=this.skinlist[this.tempid-1].bottomtar.split(";");
				this.downloadnum=this.backvideostr.length+this.bottomtarstr.length+5;
				for(let i=0;i<this.backvideostr.length;i++){
				
					this.backvideo.push({});
					}
				for(let i=0;i<this.bottomtarstr.length;i++){
					
					this.bottomtar.push("");
					}
				//下载背景图
				for(let i=0;i<this.backvideostr.length;i++){
					let j=i;
					uni.downloadFile({
						url: 'http://49.232.23.79:8081'+this.backvideostr[j], //仅为示例，并非真实的资源
						success: (res) => {
							
							if (res.statusCode === 200) {
								uni.saveFile({
									tempFilePath: res.tempFilePath,
									success: function (res) {
										
										that.backvideo[j]=res.savedFilePath;
									
										that.downloadnow++;
										that.juge();
										
									},
									fail: (res) => {
										
									}
								});
							}
						}
				});
				}
			
				//下载底部导航栏图标
				for(let j=0;j<this.bottomtarstr.length;j++){
					let i=j;
					uni.downloadFile({
						url: 'http://49.232.23.79:8081'+this.bottomtarstr[j], //仅为示例，并非真实的资源
						success: (res) => {
							if (res.statusCode === 200) {
							
								uni.saveFile({
									tempFilePath: res.tempFilePath,
									success: function (res) {
								
										if(i%2==0){
											that.bottomtar[parseInt(i/2)].image1=res.savedFilePath;				
										}
										else{
											if(that.skinlist[that.tempid-1].usesvga==1)
												that.bottomtar[parseInt(i/2)].image2='http://49.232.23.79:8081'+that.bottomtarstr[j];
											else 
												that.bottomtar[parseInt(i/2)].image2=res.savedFilePath;			
										}
										that.downloadnow++;
										that.juge();
									},
									fail: (res) => {
									
									}
								});
							}
						}
				});
				}
				//下载开屏图
				uni.downloadFile({
					url: 'http://49.232.23.79:8081'+this.skinlist[this.tempid-1].starimage, //仅为示例，并非真实的资源
					success: (res) => {
						if (res.statusCode === 200) {
							
							uni.saveFile({
								tempFilePath: res.tempFilePath,
								success: function (res) {
								
									that.starimage=res.savedFilePath;
									that.downloadnow++;
									that.juge();
									
								},
								fail: (res) => {
									
								}
							});
						}
					},
				})
				//下载首页顶部图
				uni.downloadFile({
					url: 'http://49.232.23.79:8081'+this.skinlist[this.tempid-1].backgroundimage, //仅为示例，并非真实的资源
					success: (res) => {

						if (res.statusCode === 200) {
							uni.saveFile({
								tempFilePath: res.tempFilePath,
								success: function (res) {
								
									that.backgroundimage=res.savedFilePath;
									that.downloadnow++;
									that.juge();
								}
							});
						}
					},
					fail:(res)=>{
					}
				})
				//下载装扮页面背景图
				uni.downloadFile({
					url: 'http://49.232.23.79:8081'+this.skinlist[this.tempid-1].share, //仅为示例，并非真实的资源
					success: (res) => {
					
						if (res.statusCode === 200) {
							uni.saveFile({
								tempFilePath: res.tempFilePath,
								success: function (res) {
									that.share=res.savedFilePath;
									that.downloadnow++;	
								
									that.juge();
								}
							});
						}
					},
				})
				//下载底部导航栏图标
				uni.downloadFile({
					url: 'http://49.232.23.79:8081'+this.skinlist[this.tempid-1].button, //仅为示例，并非真实的资源
					success: (res) => {
					
						if (res.statusCode === 200) {
							uni.saveFile({
								tempFilePath: res.tempFilePath,
								success: function (res) {
									that.button=res.savedFilePath;
									that.downloadnow++;	
									
									that.juge();
								}
							});
						}
					}
				})
				//下载新建主题图标
				uni.downloadFile({
					url: 'http://49.232.23.79:8081'+this.skinlist[this.tempid-1].newthemeicon, //仅为示例，并非真实的资源
					success: (res) => {
						
						if (res.statusCode === 200) {
							uni.saveFile({
								tempFilePath: res.tempFilePath,
								success: function (res) {
									that.newthemeicon=res.savedFilePath;
									that.downloadnow++;
								
									that.juge();
								}
							});
						}
					}
				})
			},
			open(){
				this.userheadimage=getApp().globalData.userheadimage;
				this.skinlist=getApp().globalData.skin;
				this.skinid=getApp().globalData.skinchoose;
				if(this.skinid!=0){
					this.color=getApp().globalData.skin[getApp().globalData.skinchoose-1].skincolor;
					this.fontcolor=getApp().globalData.skin[getApp().globalData.skinchoose-1].tabcolor;
				}
			}
		}
	}
</script>

<style>

</style>
