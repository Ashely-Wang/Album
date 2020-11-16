<template>
	<view class="login">
		<form>
			<div class="form-group">
				<label for="exampleInputEmail1">Email address</label>
				<input v-model="username" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
			</div>
			<div class="form-group">
				<label for="exampleInputPassword1">Password</label>
				<input v-model="password" type="password" class="form-control" id="exampleInputPassword1">
			</div>
			<button type="button" @click="Login" class="btn btn-primary">Submit</button>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: "",
				password: ""
			}
		},
		methods: {
			Login() {
				uni.getStorage({
					key: "userInfo",
					success: (res) => {
						// console.log(userInfo)
						// console.log(res.data)
						if (res.data.username == this.username && res.data.password == this.password) {
							uni.setStorage({
								key:"isLogin",
								data:true,
								success() {
									uni.showToast({
										title: "登录成功！"
									})
								},
								complete() {
									uni.navigateBack({})
								}
							})
							
							
							
							
						} else {
							uni.showToast({
								title: "用户名或密码错误！！"
							})
						}
					}
				})
			}
		}
	}
</script>

<style>
	@import url("https://cdn.jsdelivr.net/npm/bootstrap@4.5.0/dist/css/bootstrap.min.css");

	.login {
		width: 85%;
		position: relative;
		margin: 0 auto;
		top: 60rpx;
	}
</style>
