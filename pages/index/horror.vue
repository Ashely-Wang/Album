<template>
	<view class="content">
		<div id="horrorList">
			<div class="qqqqq">
				<div class="iteee" v-for="(item, index) in this.horrorList" :key="index">
					<img :src="item" class="img-thumbnail" alt="...">
				</div>
			</div>
		</div>
	</view>
</template>

<script>
	export default {
		data:() => {
			return {
				horrorList:[
					"https://www.tanmizhi.com/img/allimg/04/17-1P4131P237.png",
					                "http://pic.qv67.com/uploads/2018071709/20180717091188.jpg",
					                "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603702889876&di=9a7c31e7535c519ae415c5f837889ebf&imgtype=0&src=http%3A%2F%2Ff.hiphotos.baidu.com%2Fzhidao%2Fwh%253d680%252c800%2Fsign%3Df902fc893f9b033b2cddf4dc2dfe1aeb%2Fb21bb051f81986181b520e0941ed2e738bd4e622.jpg",
					                "https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=174725666,230222582&fm=26&gp=0.jpg",
					                "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1297340580,364812077&fm=26&gp=0.jpg",
					                "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3956760901,2714115272&fm=26&gp=0.jpg",
					                "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1998752008,2756127030&fm=26&gp=0.jpg",
					                "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603703246341&di=27b57306be6fd5ae868f7e3d804d5f02&imgtype=0&src=http%3A%2F%2Fwx1.sinaimg.cn%2Flarge%2F007dL8h4ly1fupnxxrylbj30m80cialm.jpg",
					                "https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1031150112,1115525191&fm=26&gp=0.jpg",
					                "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1603703606762&di=0d0926ab7e3533e713dfd75762e513c8&imgtype=0&src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farchive%2F6a4d3cb94239aae0e385613fd39111ccf90c7438.jpg",
					                "https://wx2.sinaimg.cn/mw690/006z09Zkgy1ghsq1rqyawj31hc0s84lq.jpg"
				]
			}
		}
	}
</script>

<style>
	.qqqqq {
		display: flex;
		flex-flow:column wrap;
		height: 250vh;
	}
	 .iteee {
	      margin: 10px;
	      width: calc(100%/2 - 20px);
	  }
	  .iteee img{
	      width: 100%;
	      height:100%;
	  }
</style>
