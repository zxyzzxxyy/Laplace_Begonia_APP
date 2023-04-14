<template>
	<view>
		<view style="margin-top: 5vh;;height:5vh;display: flex;justify-content: center;align-items: center;position: relative;width: 100vw;">
			<text>回复帖子</text>
			<view style="position: absolute;left:0;margin-left: 4vw;">
				<u-icon name="close" size="18" color="black"></u-icon>
			</view>
			<view style="position: absolute;right:0;margin-left: auto;margin-right: 4vw;color:#aa55ff "
			@click="huifu(1)"
			>
				回复
			</view>
		</view>
		<view style="margin-top: 20px;margin-left:2vw;width:96vw">
			<u--textarea border="none" maxlength="200" count v-model="reply" placeholder="请输入内容" autoHeight ></u--textarea>
			<u-divider></u-divider>
			<view  style="display: flex;flex-direction: row;flex-wrap: wrap;">
				<image v-for="(item,index) in uploadimages" :src="item"
				@click="deleteimage(index)" mode="aspectFill" 
				style="height:30vw;width:30vw;margin-right:1vw;margin-left: 1vw;;border-radius: 15px;margin-top:2vw"></u--image>
				<view 
				@click="uploadimage()"
				style="
					background-color: #f6faff;border:1px dashed #ecf0f4;
					height:30vw;width:30vw;margin-right:1vw;margin-left: 1vw;
					border-radius: 15px;margin-top:2vw;
					display: flex;flex-direction: column;align-items: center;justify-content:center">
					<u-icon name="plus" color="#909399" size="28"></u-icon>
					<text style="color:#909399;font-size:14px">上传图片</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				reply:"",
				themeid:0,
				uploadimages:[
				],
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
			}
		},
		onLoad(res){
			this.themeid=res.themeid;
		},
		methods: {
			huifu:function(e){
				let themeid=this.themeid;
				let that=this;
				if(this.reply.length==0&&this.uploadimages.length==0){
					this.$refs.uToast.show({
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
							this.$refs.uToast.show({
								...this.list[6],
								complete() {
								
								}
							})
						}
						else if(res.data.code==1002){
							this.$refs.uToast.show({
								...this.list[11],
								complete() {
								}
							})
						}
						else{
							this.$refs.uToast.show({
								...this.list[7],
								complete() {
								}
							})
						}
					},
					fail:(res)=>{
						this.$refs.uToast.show({
							...this.list[7],
							complete() {
							}
						})
					}
				});
			},
			deleteimage:function(e){
				this.uploadimages.splice(e,1);
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
		}
	}
</script>

<style>

</style>
