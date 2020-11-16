<template>
	<view class="setting">
		<form>
		  <div class="form-group">
		    <label for="exampleInputEmail1">Email address</label>
		    <input v-model="username" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
		  </div>
		  <div class="form-group">
		    <label for="exampleInputPassword1">Password</label>
		    <input v-model="password" type="password" class="form-control" id="exampleInputPassword1">
		  </div>
		  <button type="button" @click="setAccount" class="btn btn-primary">Submit</button>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username:"",
				password:""
			}
		},
		methods: {
			setAccount() {
				uni.setStorage({
					key:"userInfo",
					data:{username: this.username, password: this.password},
					success(res) {
						console.log(res)
						console.log("设置成功！！！")
						uni.showModal({
							title:"设置成功！！",
							content:"您可在设置页里重新定义用户名和密码",
							confirmText:"完成",
							showCancel:false,
							success() {
								uni.navigateTo({
									url:'./login'
								})
							}
						})
					}
				})
			}
		}
	}
</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.5.0/dist/css/bootstrap.min.css");
.setting {
	width: 85%;
	position: relative;
	margin: 0 auto;
	top: 60rpx;
}
</style>
