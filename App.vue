<style lang="scss">
	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
	@import "@/uni_modules/uview-ui/index.scss";
	::-webkit-scrollbar{
	      display: none;
	}
</style>
<script>
	import update from '@/uni_modules/uni-upgrade-center-app/utils/check-update.js'
	export default {
		data() {
			return {
				upload:[
					{
						type: 'success',
						icon: false,
						title: '成功主题',
						message: "设置成功",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/success.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "设置失败",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
					{
						type: 'error',
						icon: false,
						title: '成功主题',
						message: "其它设备登录",
						iconUrl: 'https://cdn.uviewui.com/uview/demo/toast/error.png',
					},
				]
			}
		},	
		globalData: {  
		    //http: "http://127.0.0.1:8806",
			http: "https://www.txtz.club:8806",
			history:[],
			tuijianguanzhu:1,
			scroll_top1:0,
			userbackgroundimage:"",
			username:"",
			scroll_top:0,
			ban:0,
			userid:-1,
			email:"",
			pixiv:[],
			userheadimage:"",
			admin:0,
			cookie:"",
			attention:[],
			mylike:[],
			firstopen:[],
			replymessage:[],
			replymessagenum:0,
			chatlist:[],
			chat:[],
			show1:false,
			xintiao:null,
			headlist:[],
			chatlistback:[],
			showpage:1,
			searchlist:[],
			skin:[],
			skinchoose:0,
		},  
		methods:{
			
			open:function(){
				
				if(getApp().globalData.cookie!='')
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
				if(getApp().globalData.cookie!='')
				{
										   
					getApp().getmychat();
					var id=0;
					if(getApp().globalData.chatlist.length!=0){
						id=getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].id;
					}
					uni.request({
					url:getApp().globalData.http+"/api/getmychatlist",
					method:"POST",
					data:{
						"id":id,
						"userid":getApp().globalData.userid,
					},
					success:(res)=>{
						for(var i=0;i<res.data.length;i++)
						getApp().globalData.chatlist.push(res.data[i]);
						//#ifdef APP-PLUS
						plus.push.addEventListener("click", function(msg) {
						    uni.reLaunch({
						    	
						
						    	url:'index?value=2'  
						    })                             
						}, false); 
						// createMessage
						var options = {cover:true};    
						var num=0;
						for(var i=0;i<res.data.length;i++){
							if(res.data[i].b==getApp().globalData.userid)
							num++;
						}
						var str = num+"条新消息";
						if(num>=1&&id!=0){
						plus.push.createMessage(str, "LocalMSG1", options);
						//plus.runtime.setBadgeNumber(num);
						}
						//#endif
						uni.setStorage({
						    key: "chatlist",
						    data: getApp().globalData.chatlist,
						    success: function () {
						    } 
						});
						getApp().connectSocketInit();
					}
					})
				}
			},
			getmychat:function(){
				uni.request({
					url:getApp().globalData.http+"/api/getmychat",
					method:"POST",
					data:{
						userid:getApp().globalData.userid,
						cookie:getApp().globalData.cookie,
						id:0
					},
					success:(res)=>{
						getApp().globalData.chat=res.data;
						for(var i=0;i<getApp().globalData.chat.length;i++)
						if(getApp().globalData.chat[i].image!=''){
							getApp().globalData.chat[i].message+="[图片]";
						}
					},
					fail:(res)=>{
						
					},
				})
			},
			send(a,b,message,image,type){
				var juge=0;
				this.socketTask.send({
					data: 
						'{"a":'+a+','+
						'"b":'+b+','+
						'"message":"'+message+'",'+
						'"image":"'+image+'",'+
						'"type":"'+type+'"'+
						'}',
					
					async success() {
						
					},
				});
			},
			
			connectSocketInit:function() {
							// 创建一个this.socketTask对象【发送、接收、关闭socket都由这个对象操作】
							this.socketTask = uni.connectSocket({
								// 【非常重要】必须确保你的服务器是成功的,如果是手机测试千万别使用ws://127.0.0.1:9099【特别容易犯的错误】
								//url: "ws://127.0.0.1:8806/api/message/"+getApp().globalData.userid,
								url: "wss://www.txtz.club:8806/api/message/"+getApp().globalData.userid,
								success(data) {
									console.log("websocket连接成功");
								},
							});
			 
							// 消息的发送和接收必须在正常连接打开中,才能发送或接收【否则会失败】
							this.socketTask.onOpen((res) => {
								console.log("WebSocket连接正常打开中...！");
								this.is_open_socket = true;
								getApp().globalData.xintiao=null;
								clearInterval(getApp().globalData.xintiao);
								this.timeoutObj = setInterval(function() {
												uni.sendSocketMessage({
													data: '{"type":"ping"}',
													success: res => {
														
													},
													fail: err => {
														console.log('连接失败重新连接....');
														getApp().connectSocketInit();
													}
												});
											}, 5000);
								// 注：只有连接正常打开中 ，才能正常成功发送消息
								
								// 注：只有连接正常打开中 ，才能正常收到消息
								this.socketTask.onMessage((res) => {
									console.log("接受到消息");
									var temp=JSON.parse((res.data));
									if(temp.type=="back"){
										getApp().globalData.chatlistback.push(temp.message);
										
										for(var i=0;i<getApp().globalData.chatlist.length;i++){
										
											if(getApp().globalData.chatlist[i].id==temp.message){
											
												getApp().globalData.chatlist.splice(i,1);
												uni.setStorage({
												    key: "chatlist",
												    data: getApp().globalData.chatlist,
												    success: function () {
												    } 
												});
												
											}
										}
										return;
									}
									getApp().getmychat();
									getApp().globalData.chatlist.push(JSON.parse((res.data)));
									
									var userid1=getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].a;
									var userid2=getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].b;
									var userid3=0;
									if(userid1==getApp().globalData.userid){
										userid3=userid2;
									}
									else{
										userid3=userid1;
									}
										uni.request({
											url:getApp().globalData.http+"/api/getusername",
											method:"POST",
											data:{
												"userid":userid3
											},
											success:(res)=>{
												var username=res.data.username;
												var imagesrc=res.data.userheadimage; 
												var juge=0;
											
												for(var i=0;i<getApp().globalData.headlist.length;i++){
													if(getApp().globalData.headlist[i].userid==userid3&&imagesrc==getApp().globalData.headlist[i].imagesrc){
													
														juge=i;break;
													}
												}
												if(juge==0&&imagesrc!=null)
												uni.downloadFile({
													url: imagesrc, //仅为示例，并非真实的资源
													success: (res) => {
														if (res.statusCode === 200) {
															uni.saveFile({ 
															      tempFilePath:res.tempFilePath,
															      success: function (res1) {
															        var savedFilePath = res1.savedFilePath
																
																	var temp={
																		"userid":userid3,
																		"userheadimage":savedFilePath,
																		"imagesrc":imagesrc,
																	}
																	var juge1=0;
																	for(var j=0;j<getApp().globalData.headlist.length;j++){
																		if(getApp().globalData.headlist[j].userid==userid3){
																			juge1=j;
																			getApp().globalData.headlist[j]=temp;
																			break;
																		}
																	}
																	if(juge1==0)
																	getApp().globalData.headlist.push(temp);
																	uni.setStorage({
																	    key: "headlist",
																	    data: getApp().globalData.headlist,
																	    success: function () {
																	    } 
																	});
																	//#ifdef APP-PLUS
																	plus.push.addEventListener("click", function(msg) {
																	    uni.reLaunch({
																	    	
																	    	url:'index?value=2'   
																	    })                             
																	}, false);  
																	var options = {cover:true,title:username,icon:savedFilePath};    
																	var str = getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].message;
																	if(getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].image!='')str+="[图片]";  
																	if(getApp().globalData.show1==true&&getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].a!=getApp().globalData.userid)					 
																	plus.push.createMessage(str, "LocalMSG", options);
																	//plus.runtime.setBadgeNumber(+1);
																	//#endif
															      }
											 				    });
														}
													
													},
													fail: (res) => {
												
													}
												});
												else if(juge!=0&&imagesrc!=null){
													//#ifdef APP-PLUS
													plus.push.addEventListener("click", function(msg) {
													    uni.reLaunch({
													    	
													    	url:'index?value=2'   
													    })                             
													}, false);  
													var options = {cover:true,title:username,icon:getApp().globalData.headlist[juge].userheadimage};    
													var str = getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].message;
													if(getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].image!='')str+="[图片]";  
													if(getApp().globalData.show1==true&&getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].a!=getApp().globalData.userid)					 
													plus.push.createMessage(str, "LocalMSG", options);
													//plus.runtime.setBadgeNumber(+1);
													//#endif
												} 
												else{
												//#ifdef APP-PLUS
												plus.push.addEventListener("click", function(msg) {
												    uni.reLaunch({
												    	
												    	url:'index?value=2'   
												    })                             
												}, false);  
												var options = {cover:true,title:username};    
												var str = getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].message;
												if(getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].image!='')str+="[图片]";  
												if(getApp().globalData.show1==true&&getApp().globalData.chatlist[getApp().globalData.chatlist.length-1].a!=getApp().globalData.userid)					 
												plus.push.createMessage(str, "LocalMSG", options);
												//plus.runtime.setBadgeNumber(+1);
												//#endif
											}
										} 
									}); 
								});
							})   
							// 这里仅是事件监听【如果socket关闭了会执行】
							this.socketTask.onClose(() => {
						
								getApp().connectSocketInit();
							})
						},
		},
		onShow:function(){
			if(getApp().globalData.cookie!=''){
			uni.request({
				url:getApp().globalData.http+"/api/jugeuser",
				method:"POST",
				data:{
					"cookie":getApp().globalData.cookie
				},
				success: (res) => {
					if(res.data.code==1002){
						uni.showToast({
							title:"其它设备登录",
							icon:"error"
						})
						getApp().globalData.username='';
						getApp().globalData.userheadimage='';
						getApp().globalData.userbackgroundimage='';
						getApp().globalData.cookie='';
						getApp().globalData.sign='';
						getApp().globalData.save='';
						getApp().globalData.bylike='';
						getApp().globalData.registertime='';
						getApp().globalData.userid='';
						getApp().globalData.admin=0;
						uni.setStorage({
						    key: "admin",
						    data: getApp().globalData.admin,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "userid",
						    data: getApp().globalData.userid,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "username",
						    data: getApp().globalData.username,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "userheadimage",
						    data: getApp().globalData.userheadimage,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "userbackgroundimage",
						    data: getApp().globalData.userbackgroundimage,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "cookie",
						    data: getApp().globalData.cookie,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "save",
						    data: getApp().globalData.save,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "bylike",
						    data: getApp().globalData.bylike,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "registertime",
						    data: getApp().globalData.registertime,
						    success: function () {
						    }
						});
						setTimeout(() => {
							uni.reLaunch({
								url:"index"
							})
						}
						, 1000)
						
					
					}
					}
				
			})}
			if(getApp().globalData.cookie!=''&&getApp().globalData.replymessage.length==0){
				var id=200000000;
				uni.request({
				url:getApp().globalData.http+"/api/getreplymessage",
				method:"POST",
				data:{
					"id":id,
					"userid":getApp().globalData.userid,
					"cookie":getApp().globalData.cookie
				},
				success:(res)=>{
					getApp().globalData.replymessage=res.data.reply;
					
				}
				})
			}
		},
		onLaunch: function() {
			uni.getSystemInfo({
				success: function (res) {
				
				}
			});
			update();
			uni.getStorage({
			    key:"skinchoose",
			    success: function(res){
			        getApp().globalData.skinchoose=res.data;
				
				}
			 });
			 uni.getStorage({
			     key:"skin",
			     success: function(res){
			         getApp().globalData.skin=res.data;
			 	
			 	}
			  });
			uni.getStorage({
			    key:"pixiv",
			    success: function(res){
			        getApp().globalData.pixiv=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			uni.getStorage({
			    key:"firstopen",
			    success: function(res){
			        getApp().globalData.firstopen=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			 uni.getStorage({
			     key:"history",
			     success: function(res){
			         getApp().globalData.history=res.data;
			 		//console.log("admin:"+getApp().globalData.admin);
			 	}
			  });
			 uni.getStorage({
			     key:"sign",
			     success: function(res){
			         getApp().globalData.sign=res.data;
			 		//console.log("admin:"+getApp().globalData.admin);
			 	}
			  });
			  uni.getStorage({
			      key:"searchlist",
			      success: function(res){
			          getApp().globalData.searchlist=res.data;
			  		//console.log("admin:"+getApp().globalData.admin);
			  	}
			   });
			 uni.getStorage({
			     key:"headlist",
			     success: function(res){
			         getApp().globalData.headlist=res.data;
			 		//console.log("admin:"+getApp().globalData.admin);
			 	}
			  });
			uni.getStorage({
			    key:"userid",
			    success: function(res){
			        getApp().globalData.userid=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			 uni.getStorage({
			     key:"cookie",
			     success: function(res){
			         getApp().globalData.cookie=res.data;
			 	
			 	}
			  });
			  uni.getStorage({
			      key:"username",
			      success: function(res){
			          getApp().globalData.username=res.data;
			  		//console.log("admin:"+getApp().globalData.admin);
			  	}
			   });
			   uni.getStorage({
			       key:"email",
			       success: function(res){
			           getApp().globalData.email=res.data;
			   		//console.log("admin:"+getApp().globalData.admin);
			   	}
			    });
				uni.getStorage({
				    key:"userheadimage",
				    success: function(res){
				        getApp().globalData.userheadimage=res.data;
						//console.log("admin:"+getApp().globalData.admin);
					}
				 });
				 uni.getStorage({
				     key:"userbackgroundimage",
				     success: function(res){
				         getApp().globalData.userbackgroundimage=res.data;
				 		//console.log("admin:"+getApp().globalData.admin);
				 	}
				  });
				  uni.getStorage({
				      key:"sign",
				      success: function(res){
				          getApp().globalData.sign=res.data;
				  		//console.log("admin:"+getApp().globalData.admin);
				  	}
				   });
				   uni.getStorage({
				       key:"registertime",
				       success: function(res){
				           getApp().globalData.registertime=res.data;
				   		//console.log("admin:"+getApp().globalData.admin);
				   	}
				    });
					uni.getStorage({
					    key:"save",
					    success: function(res){
					        getApp().globalData.save=res.data;
							//console.log("admin:"+getApp().globalData.admin);
						}
					 });
					 uni.getStorage({
					     key:"bylike",
					     success: function(res){
					         getApp().globalData.bylike=res.data;
					 		//console.log("admin:"+getApp().globalData.admin);
					 	}
					  });
					  uni.getStorage({
					      key:"replymessage",
					      success: function(res){
					          getApp().globalData.replymessage=res.data;
					  	}
					   });
					   uni.getStorage({
					       key:"chatlist",
					       success: function(res){
					           getApp().globalData.chatlist=res.data;
					   	}
					    });
						uni.getStorage({
						    key:"admin",
						    success: function(res){
						        getApp().globalData.admin=res.data;
							}
						 });
					setTimeout( () => {
							getApp().open();   
					}, 1000)
					
		
		},
		onHide: function() {
			getApp().globalData.show1=true;
	
		},
		onShow: function()  {
			getApp().globalData.show1=false;
			
			if(getApp().globalData.cookie!=''){
				uni.request({
					url:getApp().globalData.http+"/api/getmyself",
					method:"POST",
					data:{
						"cookie":getApp().globalData.cookie
					},
					success: (res) => {
						getApp().globalData.admin=res.data.data.admin;
						getApp().globalData.ban=res.data.data.ban;	
						
						uni.setStorage({
						    key: "admin",
						    data: getApp().globalData.admin,
						    success: function () {
						    }
						});
						uni.setStorage({
						    key: "ban",
						    data: getApp().globalData.ban,
						    success: function () {
						    }
						});
						uni.getStorage({
						    key:"admin",
						    success: function(res){
						        getApp().globalData.admin=res.data;
								//console.log("admin:"+getApp().globalData.admin);
							}
						 });
					}
				})
			}
			uni.getStorage({
			    key:"firstopen",
			    success: function(res){
			        getApp().globalData.firstopen=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			uni.getStorage({
			    key:"userid",
			    success: function(res){
			        getApp().globalData.userid=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			uni.getStorage({
			    key:"op",
			    success: function(res){
			        getApp().globalData.op=res.data;
					//console.log("admin:"+getApp().globalData.admin);
				}
			 });
			 uni.getStorage({
			     key:"cookie",
			     success: function(res){
			         getApp().globalData.cookie=res.data;
			 		//console.log("admin:"+getApp().globalData.admin);
			 	}
			  });
			  uni.getStorage({
			      key:"username",
			      success: function(res){
			          getApp().globalData.username=res.data;
			  		//console.log("admin:"+getApp().globalData.admin);
			  	}
			   });
			   uni.getStorage({
			       key:"email",
			       success: function(res){
			           getApp().globalData.email=res.data;
			   		//console.log("admin:"+getApp().globalData.admin);
			   	}
			    });
				uni.getStorage({
				    key:"userheadimage",
				    success: function(res){
				        getApp().globalData.userheadimage=res.data;
						//console.log("admin:"+getApp().globalData.admin);
					}
				 });
				 uni.getStorage({
				     key:"userbackgroundimage",
				     success: function(res){
				         getApp().globalData.userbackgroundimage=res.data;
				 		//console.log("admin:"+getApp().globalData.admin);
				 	}
				  });
				  uni.getStorage({
				      key:"sign",
				      success: function(res){
				          getApp().globalData.sign=res.data;
				  		//console.log("admin:"+getApp().globalData.admin);
				  	}
				   });
				   uni.getStorage({
				       key:"registertime",
				       success: function(res){
				           getApp().globalData.registertime=res.data;
				   		//console.log("admin:"+getApp().globalData.admin);
				   	}
				    });
					uni.getStorage({
					    key:"save",
					    success: function(res){
					        getApp().globalData.save=res.data;
							//console.log("admin:"+getApp().globalData.admin);
						}
					 });
					 uni.getStorage({
					     key:"bylike",
					     success: function(res){
					         getApp().globalData.bylike=res.data;
					 		//console.log("admin:"+getApp().globalData.admin);
					 	}
					  });
					  uni.getStorage({
					      key:"replymessage",
					      success: function(res){
					          getApp().globalData.replymessage=res.data;
					  	}
					   });
			if(getApp().globalData.cookie!=''&&getApp().globalData.replymessagenum==0){
				{
					var id=20000000;
					if(getApp().globalData.replymessage.length>0){
						id=getApp().globalData.replymessage[0].id;
					}
					uni.request({
						url:getApp().globalData.http+"/api/getreplymessagenum",
						method:"POST",
						data:{
							"id":id,
							"userid":getApp().globalData.userid,
							"cookie":getApp().globalData.cookie
						},
						success:(res)=>{
							getApp().globalData.replymessagenum=res.data.num;	
							if(getApp().globalData.replymessagenum>0)
							{
							uni.request({
								url:getApp().globalData.http+"/api/getreplymessage",
								method:"POST",
								data:{
									"id":200000000,
									"userid":getApp().globalData.userid,
									"cookie":getApp().globalData.cookie
								},
								success:(res)=>{
									getApp().globalData.replymessage=res.data.reply;
										uni.setStorage({
										    key: "replymessage",
										    data: getApp().globalData.replymessage,
										    success: function () {
										    }
									});
								}
							})
							}
						}
					})
				}
				
				uni.request({
					url:getApp().globalData.http+"/api/user_visit",
					method:"POST",
					data:{
						"userid":getApp().globalData.userid
					},
					success: (res) => {;
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
			}
		}
	}
</script>

<style>
	/*每个页面公共css */

</style>
