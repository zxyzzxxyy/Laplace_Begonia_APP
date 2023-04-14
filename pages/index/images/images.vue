<template>
	<view>
		<view v-if="image.length==1" 
			style="max-height:500px;border:0.3px solid #eff4fc ;border-radius: 5px;
			background-color: #eff4fc;;display: flex;align-items: center;overflow: hidden"
		>
			<image id="a1" @load="test" :src="image[0]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="min-height:100px;max-width: 92vw;min-width:25vw;" mode="widthFix"></image>
		</view>
		<view v-if="image.length==2">
			<view style="width:92vw;height:180px;display: flex;flex-direction: row;" >
				<view style="border-radius: 5px 0 0 5px;width:49.5%;height:180px;;margin-right:1%;border:0.3px solid #eff4fc ;
					background-color: #eff4fc;">
				<image id="a11"	 @load="test" :src="image[0]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="border-radius: 5px 0 0 5px;width:100%;height:180px" mode="aspectFill"></image>
				</view>
				<view style="width:49.5%;height:180px;border:0.3px solid #eff4fc ;
					background-color: #eff4fc;border-radius: 0 5px 5px 0;">
				<image id="a22"  @load="test" :src="image[1]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="border-radius: 0 5px 5px 0;width:100%;height:180px" mode="aspectFill"></image>
				</view>
			</view>
		</view>
		<view v-if="image.length>=3">
			<view style="width:92vw;height:230px;display: flex;flex-direction: row;" >
				<view style="border:0.3px solid #eff4fc ;background-color: #eff4fc;width:59%;margin-right: 1%;border-radius: 5px 0 0 5px;" >
					<image 	 @load="test" :src="image[0]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="border-radius: 5px 0 0 5px;width:100%;height:230px" mode="aspectFill"></image>
				</view>
				<view style="width:40%;display: flex;flex-direction: column;">
					<view  style="border:0.3px solid #eff4fc ;background-color: #eff4fc;width:100%;height:113.5px;margin-bottom: 3px;border-radius: 0 5px 0 0;">
					<image 	 @load="test" :src="image[1]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="width:100%;height:113.5px;border-radius: 0 5px 0 0;" mode="aspectFill"></image>
					</view>
					<view style="border:0.3px solid #eff4fc ;background-color: #eff4fc;width:100%;height:113.5px;border-radius: 0 0 5px 0;" >
					<image	@load="test" :src="image[2]+'?imageMogr2/crop/x3000/thumbnail/1000000@'" style="width:100%;height:113.5px;border-radius: 0 0 5px 0;" mode="aspectFill"></image>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			image:{
				type:Array,
				default:'',
				required:true,
			}
		},
		data() {
			return {
				images:[],
				show1:false,
				show2:false,
				show3:false,
			}
		},
		mounted(){
			
		},
		methods: {
			test(e){
				if(e.currentTarget.id=="a1"||e.currentTarget.id=="a11"||e.currentTarget.id=="a111"){
					//this.show1=true;
				}
				if(e.currentTarget.id=="a2"||e.currentTarget.id=="a22"||e.currentTarget.id=="a222"){
					//this.show2=true;
				}
				if(e.currentTarget.id=="a3"||e.currentTarget.id=="a33"||e.currentTarget.id=="a333"){
					//this.show3=true;
				}
			}
		}
		
	}
</script>

<style>
image{will-change: transform}

.a2{
	border:0.3px solid #eff4fc ;
	background-color: #eff4fc;
}
</style>
