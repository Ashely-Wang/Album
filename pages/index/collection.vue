<template>
	<view class="collection">
		<!-- <button type="default" v-if="flag4" class="btn btn-danger dele">
			<div>
				<svg @click="removeVideo(index)" width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-trash" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
				  <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
				  <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
				</svg>
			</div>
		</button> -->
		<uni-nav-bar left-text="Hey" right-icon="star" @clickRight="manage" title="Pretty Girl"></uni-nav-bar>
		<p>
		  <button @click="ic" class="scj btn btn-primary" data-toggle="collapse" href="#collapseExample" role="button" aria-expanded="false" aria-controls="collapseExample">
		    图片
		  </button>
		  <button @click="vc" class="scj btn btn-primary" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
		    视频
		  </button>
		</p>
		 <view class="">
		 	<div class="card card-body" v-show="flag1">
				<!-- <div class="qs" v-if="flag4"><label>
					<checkbox ref="qss" class="checkBox" checked="true" value="mana"/><text></text>
				</label></div> -->
		 	  <div v-for="(item, index) in videoList" :key="index" class="alert alert-success vid" role="alert" :style="style1">
				<!-- <div v-if="flag4"><label>
					<checkbox value="mana" /><text></text>
				</label></div> -->
		 	    <p @click="WatchThisVideo(index)">{{item}}</p>
				<video :src="item" v-show="rrv[index]" :ref="'video' + JSON.stringify(index)" controls></video>
		 	  </div>
		 	</div>
			<div class="card card-body" v-show="flag2">
			  <div v-for="(itemm, indexx) in imageList" :key="indexx" class="alert alert-success vid" role="alert">
			    <p @click="WatchThisImage(indexx)">{{itemm}}</p>
				<img :src="itemm" v-show="rri[indexx]" class="img-thumbnail" alt="...">
				<!-- <div class="text-center">
				  <img :src="itemm" v-for="" class="rounded" alt="...">
				</div> -->
			  </div>
			</div>
		 </view>
	</view>
</template>

<script>
	
	export default {
		data:() => {
			return{
				flag5: false,
				flag1: true,
				flag2: false,
				flag3: [false, false],
				flag4: false,
				imageList:[],
				videoList:[],
				rrv: {0:"", 1:"", 2:"", 3:"", 4:"", 5:"", 6:"", 7:"", 8:"", 9:"", 10:"", 11:"",12:"", 13:"", 14:"", 15:"", 16:""},
				rri: {0:"", 1:"", 2:"", 3:"", 4:"", 5:"", 6:"", 7:"", 8:"", 9:"", 10:"", 11:"",12:"", 13:"", 14:"", 15:"", 16:""},
				style1: {width: "100%"},
				flag6: "checked",
				items:[]
				// "vf0":false,
				// "vf1":false,
				// "vf2":false
			}
		},
		onLoad() {
			uni.getStorage({
				key:"VideoCollection",
				success:(res) => {
					console.log(res.data)
					this.videoList = res.data
					for (var i =0; i < res.data.length; i++) {
						this.rrv[i] = false
					}
				}
			})
			uni.getStorage({
				key:"ImageCollection",
				success:(res) => {
					console.log(res.data)
					this.imageList = res.data
					for (var i =0; i < res.data.length; i++) {
						this.rri[i] = false
					}
				}
			})
		},
		methods:{
			qbs(e) {
				
				// console.log(qq[0].getAttribute("checked"))
				// console.log(this.$refs.qs.value)
				// if (this.$refs.qs.checked == true) {
					
				// } else {
				// 	console.log("rrrrrr")
				// }
				
			},
			manage() {
				if (this.flag4 == true) {
					this.style1 = {width: "100%"}
				} else {
					this.style1 = {width: "92%"}
				}
				this.flag4 = !this.flag4
			},
			checkVideo: (e) => {
				return true
			},
			checkImage: (e) => {
				return true
			},
			ic() {
				this.flag1 = false
				this.flag2 = true
			},
			vc() {
				this.flag1 = true
				this.flag2 = false
			},
			WatchThisVideo(e) {
				this.rrv[e] = !this.rrv[e]
				for (var i =0; i < this.videoList.length; i++) {
					if (i != e) {
						this.rrv[i] = false
					}				
				}
			},
			WatchThisImage(e) {
				this.rri[e] = !this.rri[e]
				for (var i =0; i < this.imageList.length; i++) {
					if (i != e) {
						this.rri[i] = false
					}				
				}
			},
			removeVideo(e) {
				var u = []
				// var u = ["sd", "das", "gggg", "yuu"]
				// u.splice(0,1)
				// console.log(u)
				this.videoList.splice(e,1)
				uni.setStorage({
					key:"VideoCollection",
					data:this.videoList,
					success(res) {
						console.log("取消收藏成功！！！")
					}
				})
			},
			removeImage(e) {
				
			}
		}
	}
</script>

<style>
	@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.5.0/dist/css/bootstrap.min.css");
	.scj {
		width: 34.5%;
		margin-left: 50rpx;
		margin-top: 32rpx;
	}
	.vid {
		position: relative;
		/* left: -5rpx; */
	}
	.vid>div {
		position: absolute;
		right: -76rpx;
		top: 38%;
		width: fit-content;
		height: fit-content;
	}
	.dele {
		width: 100%;
		position: fixed;
		bottom: 0rpx;
		z-index: 3;
		font-size: 23rpx;
		background-color: #dc3545;
	}
	.card {
		position: relative;
	}
	.qs {
		position: absolute;
		top: -5rpx;
		right: 30rpx;
	}
</style>
