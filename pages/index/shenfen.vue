<template>
	<view style="height: 95vh;background-color: white;">
		<view style=";height:4vh;margin-bottom:10px;;padding-top: 5vh;" :style="{backgroundColor:color}">
			<view style="display: flex;flex-direction: row;align-items: center;margin-left: 2vw;" >
			<view @click="back">
			<u-icon name="arrow-left"  size="23" :color="color1" ></u-icon>
			</view>
			<view @click="save" style="margin-left: auto;margin-right: 5%;" :style="{color:color1}">
				<text>保存</text>
			</view>
			</view>
		</view>
		<view style="padding-top: 1rem;padding-bottom: 1rem;padding-left: 0.5rem;padding-right: 0.5rem;background-color: aliceblue;margin-top: 1px solid #909399;">
			<view>
				<text style="font-size: 14px;color:#909399">我的身份标签({{myidentity.length}}/3)</text>
			</view>
			<view style="margin-top: 1rem;font-size: 14px;">
				<text>身份标签会显示在个人主页，评论区等页面，让你更容易找到同好</text>
			</view>
			<view style="display: flex;flex-direction: row;flex-wrap: warp;">
			<view v-for="(item,index) in myidentity" style="margin-top: 1rem;">
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.identity"  
	v-if="item.identity!=null" @click="deleteshenfen1(index)"> </u-tag>
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.interest"
	v-if="item.interest!=null" @click="deleteshenfen1(index)"> </u-tag>
			</view>
			</view>
		</view>
		<view style="padding-top: 1rem;padding-bottom: 1rem;padding-left: 0.5rem;padding-right: 0.5rem;background-color: white;margin-top: 1px solid #909399;" v-if="show1">
			<view>
				<text style="font-size: 14px;color:#909399">我的技能</text>
			</view>
			<view style="display: flex;flex-direction: row;flex-wrap: wrap;">
				<view v-for="(item,index) in identity">
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.identity" plain  v-if="!jugeidentity(index)"
				@click="addshenfen(index,1)"
				> </u-tag>
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.identity"   v-if="jugeidentity(index)"
				@click="deleteshenfen(index,1)"
				> </u-tag>
				</view>
			</view>
		</view>
		<view style="padding-top: 1rem;padding-bottom: 1rem;padding-left: 0.5rem;padding-right: 0.5rem;background-color: white;margin-top: 1px solid #909399;" v-if="show1">
			<view>
				<text style="font-size: 14px;color:#909399">我的兴趣</text>
			</view>
			<view style="display: flex;flex-direction: row;flex-wrap: wrap;">
				<view v-for="(item,index) in interest">
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.interest" plain  v-if="!jugeinterest(index)"
				@click="addshenfen(index,2)"
				> </u-tag>
				<u-tag style="margin-top: 0.5rem;margin-right: 10px;"  :text="item.interest"   v-if="jugeinterest(index)"
				@click="deleteshenfen(index,2)"
				> </u-tag>
				</view>
			</view>
		</view>
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
		import MiddleUtil from '@/pages/index/MiddleUtil.js';
	export default {
		data() {
			return {
				myidentity:[],
				identity:[],
				color:"white",
				color1:"black",
				interest:[],
				show1:false,
				list:[
					{
						type: 'success',
						icon: false,
						title: '成功主题',
						message: "保存成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
					{
						type: 'error',
						icon: false,
						title: '失败主题',
						message: "保存失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png'
					},
				],
			}
		},
		onLoad() {
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
				url:getApp().globalData.http+"/api/getshenfenlist",
				method:"POST",
				data:{
					
				},
				success: (res) => {
					this.identity=res.data[0];
					this.interest=res.data[1];
					uni.request({
						url:getApp().globalData.http+"/api/getmyshenfen",
						method:"POST",
						data:{
							"userid":getApp().globalData.userid
						},
						success: (res) => {
							for(var i=0;i<res.data.length;i++){
								
								if(res.data[i].type==1){
									var identity="";
									for(var j=0;j<this.identity.length;j++){
									
										if(this.identity[j].id==res.data[i].id){
											identity=this.identity[j].identity;
											break;
										}
									}
									
									var temp={
										"id":res.data[i].id,
										"type":res.data[i].type,
										"identity":identity
									}
									this.myidentity.push(temp);
								}
								else{
									var interest="";
									for(var j=0;j<this.interest.length;j++){
								
										if(this.interest[j].id==res.data[i].id){
											interest=this.interest[j].interest;
											break;
										}
									}
									var temp={
										"id":res.data[i].id,
										"type":res.data[i].type,
										"interest":interest
									}
									this.myidentity.push(temp);
								}
							}
							this.show1=true;
						},
						
					})
				}
			})
			
		},
		methods: {
			save:function(){
				var temp=[];
				let that=this;
				for(var i=0;i<this.myidentity.length;i++){
					temp.push({
						"type":this.myidentity[i].type,
						"id":this.myidentity[i].id
					})
				}
				uni.request({
					url:getApp().globalData.http+"/api/setmyshenfen",
					method:"POST",
					data:{
						"data":temp,
						"userid":getApp().globalData.userid
					},
					success: (res) => {
						if(res.data.code==1001){
							this.$refs.uToast.show({
							...this.list[0],
							complete() {
								MiddleUtil.$emit('getmyslef','');
								that.back();
							}})
						}
						else{
							this.$refs.uToast.show({
							...this.list[1],
							complete() {
								
							}})
						}
					},
					fail: (res) => {
						this.$refs.uToast.show({
						...this.list[1],
						complete() {
							
						}})
					}
				})
			},
			back(){
				uni.navigateBack({
					delta:1
				})
			},
			deleteshenfen1:function(e){
				this.myidentity.splice(e,1);
			},
			deleteshenfen:function(index,type){
				if(type==1){
					for(var i=0;i<this.myidentity.length;i++){
						if(this.myidentity[i].type==1){
							if(this.myidentity[i].id==this.identity[index].id)
								this.myidentity.splice(i,1);
						}
					}
				}
				else{
					for(var i=0;i<this.myidentity.length;i++){
						if(this.myidentity[i].type==2){
							if(this.myidentity[i].id==this.interest[index].id)
								this.myidentity.splice(i,1);
						}
					}
				}
			},
			addshenfen:function(index,type){
				if(this.myidentity.length==3)return;
				if(type==1){
					this.identity[index].type=1;
					var temp=this.identity[index];
				
					this.myidentity.push(temp);
				}
				else{
					this.interest[index].type=2;
					var temp=this.interest[index];
					this.myidentity.push(temp);
				}
			},
			jugeidentity:function(e){
				for(var i=0;i<this.myidentity.length;i++){
					
					if(this.myidentity[i].type==1){
						if(this.myidentity[i].id==this.identity[e].id){
							//console.log(this.myidentity[i]);
							return true;
						}
					}
				}
				return false;
			},
			jugeinterest:function(e){
				for(var i=0;i<this.myidentity.length;i++){
					if(this.myidentity[i].type==2){
						if(this.myidentity[i].id==this.interest[e].id){
						//	console.log(this.myidentity[i]);
							return true;
						}
					}
				}
		
				return false;
			}
		}
	}
</script>

<style>

</style>
