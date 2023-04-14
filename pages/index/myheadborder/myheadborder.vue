<template>
	<view>
		<view style="display: flex;flex-direction: row;flex-wrap: wrap;margin-top:10px">
		
		<view style="width:100%;display: flex;justify-content: center;margin-top: 50px;margin-bottom: 50px;">
			<view v-for="(item,index) in headborderlist">
			<userhead
			
			style=" margin-bottom:10px;width:40px;height:40px;margin-left:5px;margin-right:5px;" 
			:type="1"
			:size="'100'" :username="username" 
			:userheadimage="userheadimage"
			:headborder="item.url" 
			:pianyi="item"
			v-if="headborderid==item.id&&headborderid!=0"
					
			></userhead>
			</view>
			<userhead
			
			style=" margin-bottom:10px;width:40px;height:40px;margin-left:5px;margin-right:5px;" 
			:type="1"
			:size="'100'" :username="username" 
			:userheadimage="userheadimage"
			v-if="headborderid==0"
					
			></userhead>
			
		</view>	
		<view style="display: flex;flex-direction: row;justify-content:center;;flex-wrap: wrap;width:100vw">
		<view v-for="(item,index) in headborderlist" style="">
			<view 	@click="setuserheadborder(item)">
			<userhead  
			
			style=" margin-bottom:10px;width:40px;height:40px;margin-left:5px;margin-right:5px;border:1px solid #cfd4dc;padding:35px;border-radius: 15px;" 
			:type="1"
			:size="'60'" :username="username" 
			:userheadimage="userheadimage1"
			:headborder="item.url" 
			:pianyi="item"
				v-if="headborderid!=item.id"
		
			></userhead>
			</view>
			<view 	@click="setuserheadborder({id:0})">
			<userhead
		
			style=" margin-bottom:10px;width:40px;height:40px;margin-left:5px;margin-right:5px;border:1px solid #3c9cff;padding:35px;border-radius: 15px;" 
			:type="1"
			:size="'60'" :username="username" 
			:userheadimage="userheadimage1"
			:headborder="item.url" 
			:pianyi="item"
			v-if="headborderid==item.id"
			></userhead>
			</view>
		</view>
		<view v-if="headborderlist.length%3!=0" v-for="i in 3-headborderlist.length%3" style=" margin-bottom:10px;width:40px;height:40px;margin-left:5px;margin-right:5px;border:1px none #cfd4dc;padding:35px;border-radius: 15px;" >
		</view>	
		</view>
		</view>
		<u-divider></u-divider>
		<view style="display: flex;flex-direction: column;align-items: center;justify-content: center;width:100vw;margin-top:10px"
		
		>
			<text style="font-size: 14px;color:#909399">没有更多了</text>
		</view>
	
	</view>
</template>

<script>
	import userhead from "../userhead/userhead.vue"
	export default {
		components:{
			userhead
		},
		data() {
			return {
				
				headborderlist:[],
				userid:0,
				headborderid:-1,
				username:"",
				userheadimage:"",
				userheadimage1:'../../../static/1234.jpg',
			}
		},
		onLoad() {
			this.userid=getApp().globalData.userid;
			this.username=getApp().globalData.username;
			this.userheadimage=getApp().globalData.userheadimage;
			uni.request({
				url:getApp().globalData.http+"/api/myheadborderlist",
				method:"POST",
				data:{
					userid:this.userid
				},success: (res) => {
					this.headborderlist=res.data.list;
					this.headborderid=res.data.headborderid;
				}
			})
		},
		methods: {
			setuserheadborder(e){
				uni.request({
					url:getApp().globalData.http+"/api/setuserheadborder",
					method:"POST",
					data:{
						userid:this.userid,
						headborderid:e.id
					},success: (res) => {
						if(res.data.code==1001)this.headborderid=e.id;
					}
				})
			}
		}
	}
</script>

<style>

</style>
