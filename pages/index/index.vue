<template>
	<view class="content">
		<uni-nav-bar left-text="Hey" right-icon="star" @clickLeft="logout" @clickRight="toCollection" title="Pretty Girl"></uni-nav-bar>
		<view class="add_image">
			<button @click="addImage" type="default">Add</button>
		</view>
		<view class="tttt">
			<video :src="currentVideo" autoplay="true" controls></video>
		</view>
		<view class="vieo">
			<button class="btn btn-primary" @click="changeVideo" type="default">换一个</button>
			<button class="btn" @click="collect" type="default">收藏</button>
		</view>
		<div id="girlList">
			<div class="qqq">
				<div class="ite" v-for="(item, index) in this.girlList" :key="index">
					<img @click="checkImage(item)" :src="item" class="img-thumbnail" alt="...">
				</div>
			</div>
		</div>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		data() {
			return {
				videoList: [
					"https://cdn.ggac.net/media/work/video/2020/04/08e04d52-7a2a-11ea-be68-0242c0a82002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/06/e1a2222c-a76c-11ea-b3c1-0242c0a82002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/06/f9ea738e-b24d-11ea-8d66-0242c0a88002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/10/4a53486a-1620-11eb-bc93-0242c0a82002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/10/5a12ed4c-16ba-11eb-89ea-0242c0a88002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/10/8108b0e4-182c-11eb-92fa-0242c0a82002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/10/0068e7c2-1540-11eb-b4e3-0242c0a82002.mp4",
					"https://cdn.ggac.net/media/work/video/2020/04/248c4aea-85c1-11ea-9e20-0242c0a88002.mp4",
					"https://cdn.ggac.net/media/work/video/2019/11/c0f384be-12cd-11ea-bbe1-0242c0a88002.mp4"
					
				],
				currentVideo: "https://cdn.ggac.net/media/work/video/2020/04/08e04d52-7a2a-11ea-be68-0242c0a82002.mp4",
				imageChossed: "",
				girlList: [
					"https://c-ssl.duitang.com/uploads/item/202003/01/20200301221914_zwJzP.thumb.1000_0.jpeg",
					            'https://c-ssl.duitang.com/uploads/item/202003/21/20200321211316_enmpm.thumb.1000_0.jpeg',
					            "https://c-ssl.duitang.com/uploads/item/202003/21/20200321211228_lgtrk.thumb.1000_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202003/27/20200327142814_igbcs.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202006/19/20200619150827_2QNdT.thumb.1000_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202001/23/20200123222530_jdram.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202002/22/20200222111242_uukml.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/201711/29/20171129001425_sracf.thumb.400_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202004/07/20200407160128_etduv.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/201910/23/20191023152135_kmwjl.thumb.400_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202007/13/20200713205310_eckmd.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202006/22/20200622170829_prcgr.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/blog/202009/23/20200923220612_9903e.thumb.1000_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202003/13/20200313170139_riwog.thumb.1000_0.jpg",
					"https://wxt.sinaimg.cn/mw1024/67798908gy1fhj8b8o12bj20mq0yqap0.jpg?tags=%5B%5D",
					"https://wx1.sinaimg.cn/mw1024/67798908gy1fhj8b4jvkjj20nm0z4gvm.jpg",
					            // "https://c-ssl.duitang.com/uploads/item/202006/30/20200630173734_rdord.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/blog/202008/11/20200811215359_axlww.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/201910/06/20191006215119_yoeke.thumb.400_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/201705/13/20170513075031_kuBZP.thumb.400_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202006/17/20200617154226_djuni.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202008/07/20200807213900_mcdcf.thumb.1000_0.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202003/07/20200307121149_NmxMN.thumb.1000_0.jpeg",
					            "https://img.zcool.cn/community/01cfa558e492f6a801219c77863db2.jpg@1280w_1l_2o_100sh.jpg",
					            "https://img.zcool.cn/community/011c195542deb10000019ae9a52fd5.jpg@1280w_1l_2o_100sh.jpg",
					            "https://img.zcool.cn/community/01588655419f5e000001a64b92a0bd.jpg@1280w_1l_2o_100sh.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202003/22/20200322140717_uhgbq.thumb.1000_0.jpg",
					            // "https://c-ssl.duitang.com/uploads/item/202008/21/20200821171940_xHnzN.thumb.1000_0.jpeg",
					            "https://c-ssl.duitang.com/uploads/item/202006/28/20200628195611_zXHZe.thumb.1000_0.jpeg",
					            "https://wx2.sinaimg.cn/mw1024/ec432dc9gy1ghcsbpct6sj21461jknpd.jpg",
					            "https://wx2.sinaimg.cn/mw1024/ec432dc9gy1gamzfifrbkj20sd15o4pw.jpg",
					            "https://wx1.sinaimg.cn/mw1024/ec432dc9gy1fuiajm6pspj20zk1eb7wh.jpg",
					            "https://wx2.sinaimg.cn/mw1024/ec432dc9ly1fnv44gd10qj20qw15o7lh.jpg",
					            "https://wx3.sinaimg.cn/mw1024/ec432dc9gy1fvii8f2gtnj20zr1ekkjl.jpg",
					            "https://hbimg.huabanimg.com/e760f3df1ac5c96fbd9dbb7ab57ef44f28b1efc9291244-nCFCVB_fw658/format/webp",
					            "https://i0.hdslb.com/bfs/article/ff0368d7eafb9b1cb7a90863e985ccd3de073db3.jpg@1320w_986h.webp",
					            "https://i0.hdslb.com/bfs/article/6c7aab35aba829070f09e5d08f68154db08cfdeb.jpg@1320w_814h.webp",
					            // "https://c-ssl.duitang.com/uploads/item/202005/14/20200514210712_qdywt.thumb.1000_0.png",
					            "https://cdn.ggac.net/media/work/image/2020/09/bba0aaae-0166-11eb-ab55-0242c0a88002.jpg",
					            "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603366219665&di=0dbf1179f12aa41200a2fe366d7c7664&imgtype=0&src=http%3A%2F%2Fs.lanqb.com%2F20160411%2F1460368791-c-1378x1034.jpg",
					            "https://c-ssl.duitang.com/uploads/blog/202010/10/20201010221930_0c78b.thumb.1000_0.jpg",
					            "https://img.zcool.cn/community/0139005ab88c7ca80120be14e59de4.jpg@1280w_1l_2o_100sh.jpg",
					            "https://c-ssl.duitang.com/uploads/item/202008/27/20200827234508_hlvlf.thumb.1000_0.jpg",
					            "https://hbimg.huabanimg.com/a1d6716ff3ad63b0d9e81f7ba262eed9e86315b21876c-yEnMiz_fw658/format/webp",
					            "https://hbimg.huabanimg.com/454bb1b3bc64b076b8afa20a9a55ec4033f4bb3283a9eb-WdCm1H_fw658/format/webp",
					            "https://cdn.ggac.net/media/work/image/2020/05/92aeb748-95a6-11ea-940d-0242c0a82002.jpg",
					            "https://cdn.ggac.net/media/work/image/2019/10/a07cafa4-e8d8-11e9-a89d-0242c0a82003.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/10/84cd92aa-0e8e-11eb-8df2-0242c0a84002.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/10/21aaa4cc-0a62-11eb-8f43-0242c0a88002.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/10/036463f6-1406-11eb-8757-0242ac110002.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/10/7cd0ae54-1085-11eb-8a18-0242c0a82002.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/10/41521208-0489-11eb-b462-0242c0a82002.jpg",
					            "https://cdn.ggac.net/media/work/image/2020/09/e80983ae-f324-11ea-9d03-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/10/71313dd4-0932-11eb-afce-0242c0a82002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/10/a0d54a54-0931-11eb-9beb-0242c0a82002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/10/805eb80c-0605-11eb-8759-0242c0a82002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/09/37335f58-ffc9-11ea-b2aa-0242c0a88002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/07/3afb8e78-bc38-11ea-ac9d-0242c0a84002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/09/64257ad2-fd3f-11ea-b96e-0242c0a88002.gif",
					                "https://cdn.ggac.net/media/work/image/2020/09/39504cd4-fd3e-11ea-8835-0242c0a88002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/09/78629334-fc0b-11ea-b96e-0242c0a88002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/09/9b40c5a6-f805-11ea-95d6-0242ac110002.jpg",
					                "https://cdn.ggac.net/media/work/image/2020/09/064cffc2-f59a-11ea-a4d5-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/04/c4d94a96-887a-11ea-b620-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/09/79c7f9ce-f406-11ea-9f93-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/09/60bc913a-f4f4-11ea-9fab-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/09/0ef8d776-eddf-11ea-bb46-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/06/0cdb96f2-b0ab-11ea-84cd-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/5fb5d690-e7c3-11ea-a886-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/2d6f5ece-e4a1-11ea-bec2-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/09/28731548-f63d-11ea-95c5-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/02940ea2-e609-11ea-a704-0242c0a84002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/9a05b7f4-db9b-11ea-8212-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/ae1445ea-d78a-11ea-b13d-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/7e8aef7e-d6e8-11ea-83a2-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/5ca888c6-d6bb-11ea-8016-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/be055ecc-d62b-11ea-b54b-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/20c3997a-d2f3-11ea-a80f-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/a5a79834-d13c-11ea-9e65-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/3c0c14ea-cefd-11ea-8e05-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/d9756174-cefc-11ea-922b-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/c6784280-cefc-11ea-9edb-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/a23d944e-cc93-11ea-83e0-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/07/0e114e58-cb05-11ea-9edb-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/c0fc3b7c-dacd-11ea-a5e3-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/06/a9a1239e-b74a-11ea-9c9f-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/06/c2ca0d2c-b39e-11ea-8a3e-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/06/58905b96-b39e-11ea-adf8-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2019/10/86372a4c-eb40-11e9-9b81-0242c0a84002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/05/89e20904-9fe1-11ea-8f61-0242c0a84002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/05/5a2921c2-9b43-11ea-a048-0242c0a88002.jpg",
									"https://img.cgmodel.com/image/2020/1009/big/541028-1623791380.jpg",
									"https://img.cgmodel.com/image/2020/0914/big/1035238-659583644.png",
									"https://img.cgmodel.com/image/2020/0907/big/1099791-1354114065.jpg",
									"https://img.cgmodel.com/image/2020/0824/big/1521217-1474247249.jpg",
									"https://img.cgmodel.com/image/2019/1017/big/1021349-927702678.jpg",
									"https://img.cgmodel.com/image/2020/0811/big/1327252-2143746603.jpg",
									"https://img.cgmodel.com/image/2020/0726/big/1238057-681664316.jpg",
									"https://img.cgmodel.com/image/2020/0619/big/960600-381444486.jpg",
									"https://img.cgmodel.com/image/2020/0609/big/1479459-1044801164.jpg",
									"https://img.cgmodel.com/image/2020/0512/big/1473001-291496704.jpg",
									"https://cdn.ggac.net/media/work/image/2019/09/88685a0a-e345-11e9-964e-0242c0a82003.jpg",
									"https://cdn.ggac.net/media/work/image/2019/09/51cd2a00-cdf8-11e9-bab7-0242c0a88002.jpg",
									"https://cdn.ggac.net/media/work/image/2019/12/fa957232-2bdb-11ea-a59a-0242c0a82002.jpg",
									"https://cdn.ggac.net/media/work/image/2020/08/6d866f7a-d7db-11ea-80b2-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/08/5712f2ee-dd81-11ea-a07f-0242c0a84002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/09/d1adeffc-fd40-11ea-a201-0242c0a88002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/06/e8420ce0-a727-11ea-87e7-0242c0a88002.jpg",
					"http://www.gyxy.cn/uploadfile/image/20200814/20200814165843_48532.jpg",
					"http://www.gyxy.cn/uploadfile/image/20200203/20200203145210_33258.jpg",
					"http://www.gyxy.cn/prosimg/20170828088302858.jpg",
					"https://cdn.ggac.net/media/work/image/2020/06/0c52cce6-a656-11ea-95ca-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/09/15e90cec-f32d-11ea-8d67-0242ac110002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/09/0341792c-f32c-11ea-92b2-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/05/1004bb48-9b42-11ea-b6ba-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2020/10/c5076518-1932-11eb-a665-0242c0a82002.jpg",
					"https://w.wallhaven.cc/full/lm/wallhaven-lm3132.jpg",
					"https://w.wallhaven.cc/full/w8/wallhaven-w8wplr.jpg",
					"https://w.wallhaven.cc/full/g8/wallhaven-g81wo7.jpg",
					"https://w.wallhaven.cc/full/2e/wallhaven-2eqgqy.jpg",
					"https://w.wallhaven.cc/full/zm/wallhaven-zm1rgj.jpg",
					"https://w.wallhaven.cc/full/ym/wallhaven-ymz9mk.jpg",
					"https://cdn.ggac.net/media/work/image/2019/09/35a9a22a-dff7-11e9-a91c-0242c0a82003.jpg",
					"https://cdn.ggac.net/media/work/image/2019/10/e9733cd2-e8e7-11e9-ae6e-0242c0a84002.jpg",
					"https://cdn.ggac.net/media/work/image/2019/08/eec0ee74-b8cb-11e9-bbc1-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2019/10/065ded1c-e913-11e9-8dc7-0242c0a82003.jpg",
					"https://cdn.ggac.net/media/work/image/2019/05/622e7138-753d-11e9-84b4-0242c0a82002.jpg",
					"https://cdn.ggac.net/media/work/image/2019/09/589fb940-e38f-11e9-93bd-0242c0a84002.jpg",
					"https://cdn.ggac.net/media/work/image/2019/10/2a153f74-e44c-11e9-93bd-0242c0a84002.jpg"

				],
			}
		},
		onLoad() {
			uni.getStorage({
				key: "isLogin",
				success(res) {
					if (res.data == false) {
						uni.getStorage({
							key: "userInfo",
							success() {
								console.log("未登录  但是有帐号信息")
								uni.navigateTo({
									url: "./login"
								})
							},
							fail() {
								console.log("未登录  并且无帐号信息")
								uni.navigateTo({
									url: "./sign"
								})
							}
						})
					} else {
						console.log("已登陆啦")
					}
				},
				fail(err) {
					console.log("无登录信息")
					uni.getStorage({
						key: "userInfo",
						success() {
							uni.navigateTo({
								url: "./login"
							})
						},
						fail() {
							uni.navigateTo({
								url: "./sign"
							})
						}
					})
				}
			})
		},
		components: {
			uniNavBar
		},
		methods: {
			checkImage(e) {
				// console.log(e)
				var indexI = this.girlList.indexOf(e)
				uni.navigateTo({
					url: `./checkTheImage?id=${indexI}`
				})
			},
			logout() {
				uni.setStorage({
					key: "isLogin",
					data: false,
					success() {
						uni.navigateTo({
							url: "./login"
						})
					}
				})
			},
			addImage() {
				uni.navigateTo({
					url: "./sign"
				})
				// ###############################################################################################
				// uni.getStorage({
				// 	key:"VideoCollection",
				// 	success:(res) => {
				// 		console.log(res.data)
				// 	},
				// 	fail(err) {
				// 		console.log("has been cleared")
				// 	}
				// })
				// uni.clearStorage()
				// uni.getStorage({
				// 	key:"VideoCollection",
				// 	success:(res) => {
				// 		console.log(res.data)
				// 	},
				// 	fail(err) {
				// 		console.log("has been cleared")
				// 	}
				// })
				// ###############################################################################################
				// uni.previewImage({
				// 	urls:["https://cdn.ggac.net/media/work/image/2020/05/77112772-9b3d-11ea-8865-0242c0a88002.jpg"]
				// })
				// ###############################################################################################
				// uni.chooseImage({
				// 	count:5,
				// 	sourceType:["album"],
				// 	success:(e) => {
				// 		// console.log(JSON.parse(JSON.stringify(e.tempFilePaths)))
				// 		console.log(e.tempFiles[0].path)
				// 		// this.imageChossed = e.tempFiles[0].path
				// 		this.girlList.push(e.tempFiles[0].path)
				// 		// this.girlList.push(e.tempFilePaths.blob)
				// 	}
				// })
				// ###############################################################################################
				// uni.chooseImage({
				//     count: 1,
				//     sourceType: ['camera'],
				//     success: function (res) {
				//         uni.saveImageToPhotosAlbum({
				//             filePath: res.tempFilePaths[0],
				//             success: function () {
				//                 console.log('save success');
				//             }
				//         });
				//     }
				// });
			},
			collect() {
				var formerData = []
				uni.getStorage({
					key: "VideoCollection",
					success: (res) => {
						formerData = res.data
						if (res.data.indexOf(this.currentVideo) != -1) {
							console.log("收藏夹已存在！！！")
						} else {
							console.log(formerData)
							formerData.push(this.currentVideo)
							console.log(formerData)
							uni.setStorage({
								key: "VideoCollection",
								data: formerData,
								success: (resp) => {
									console.log(resp)
									console.log("收藏成功！！")
								}
							})
						}
					},
					fail: (err) => {
						console.log("no data")
						console.log(formerData)
						formerData.push(this.currentVideo)
						console.log(formerData)
						uni.setStorage({
							key: "VideoCollection",
							data: formerData,
							success(resp) {
								console.log(resp)
								console.log("收藏成功！！")
							}
						})
					}
				})
				// uni.setStorage({
				// 	key:"VideoCollection",
				// 	data:[""]
				// })
			},
			changeVideo() {
				var videoIndex = this.videoList.indexOf(this.currentVideo)
				if (videoIndex == 6) {
					this.currentVideo = this.videoList[0]
				} else {
					this.currentVideo = this.videoList[videoIndex + 1]
				}
			},
			toCollection() {
				uni.navigateTo({
					url: "./collection"
				})
			}

		}
	}
</script>

<style>
	@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.5.0/dist/css/bootstrap.min.css"integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk");


	.qqq {
		display: flex;
		flex-flow: column wrap;
		height: 2400vh;
	}

	.ite {
		margin: 10px;
		width: calc(100%/2 - 20px);
	}

	.ite img {
		width: 100%;
		height: 100%;
	}

	.tttt video {
		width: 100%;
	}

	.vieo button {
		width: 48%;
		margin-left: 8rpx;
	}
</style>
