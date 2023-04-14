<template>
	<view style="position: relative;display: flex;align-items: center;justify-content: center">
		<u-avatar defaultUrl=""  style="position:absolute;z-index: 1;" mode="aspectFill":src="userheadimage" v-if="userheadimage!=''&&userheadimage!=null" :size="size"></u-avatar>
		<u-avatar defaultUrl=""  style="position:absolute;z-index: 1;" :text="username.substr(0,1)"  randomBgColor v-if="userheadimage==''||userheadimage==null" :size="size"></u-avatar>
		<u--image 
		loadingIcon=" " errorIcon=" " :showLoading="false" :showError="false"
		:style="{marginLeft:pianyi.left+'px',marginTop:pianyi.top+'px'}"
		:lazyLoad="false" :fade="false" v-if="headborder!=''&&headborder!=null&&type==1" style="x;position:absolute;z-index: 2;" :width="test(size)+'px'" :height="test(size)+'px'" 
		:src="headborder.toString()+'?imageMogr2/thumbnail/300x300'"></u--image>
		<u--image 
		loadingIcon=" " errorIcon=" " :showLoading="false" :showError="false"
		:style="{marginLeft:pianyi.left1+'px',marginTop:pianyi.top1+'px'}"
		:lazyLoad="false" :fade="false" v-if="headborder!=''&&headborder!=null&&type==0" style="x;position:absolute;z-index: 2;" :width="test(size)+'px'" :height="test(size)+'px'" 
		:src="headborder.toString()+'?imageMogr2/thumbnail/300x300'"></u--image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				key:"",
				op:1,
				//icon:"../../static/icon.png",
				icon:"../../static/1.jpg",
				searchtuijian:"",
			}
		},
		props:{
			username:{
				type:String,
				default:'',
				required:true
			},
			userheadimage:{
				type:String,
				default:'',
				required:true
			},
			headborder:{
				type:String,
				default:'',
				required:true
			},
			size:{
				type:String,
				default:"38",
				required:false
			},
			pianyi:{
				type:Object,
				
				required:true
			},
			type:{
				type:Number,
				default:0,
				require:false
			}
		},
		watch:{
			 type: {
			    　　handler(newName, oldName) {
			     
			    　　},
			    　　immediate: true
			    }
		},
		methods: {
			test(e){
				
				let i=0;
				if(this.type==1){
				return parseInt(e)+parseInt(this.pianyi.pianyi1);
				}
				else
				return parseInt(e)+this.pianyi.pianyi;
			}
		}
	}
</script>

<style>

</style>
