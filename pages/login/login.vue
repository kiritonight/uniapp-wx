<template>
	<view class="content">
		<view class="logodiv">
			<view class="logo">
				<image class="imglogo" src="../../static/logo.png" mode="widthFix"></image>
			</view>
		</view>
		<view class="form">
			<view class="username">
				<input class="nameform" type="text" v-model="username" placeholder="请输入用户名" />
			</view>
			<view class="password">
				<input class="pawform" type="password" v-model="password" placeholder="请输入密码" />
			</view>
			<view class="loginBtn" hover-class="loginBtnhover" @tap="loginrequest">
				<text class="btnvalue">登录</text>
			</view>
			<view class="registBtn">
				<text class="regist" @tap="gotoregist">注册用户</text>
				<text>|</text>
				<text class="user" @tap="gotouser">返回首页</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username:'',
				password:'',
			}
		},
		methods: {
			gotouser(){
				uni.switchTab({
					url:"../user/user"
				})
			},
			gotoregist(){
				uni.navigateTo({
					url:"./regist"
				})
			},
			loginrequest(){
				uni.request({
					url: 'http://127.0.0.1:8088/robot/user/login',
					method: 'POST',
					data: {
						username:this.username,
						password:this.password,
					},
					header:{
						"content-type":"application/x-www-form-urlencoded"
					},
					success: res => {
						console.log(res);
						if(res.data.status){	
							 uni.reLaunch({
							    url:"../user/user",
							}),
							uni.showToast({
								title:res.data.message,
								icon:"loading"
							}),
							uni.setStorageSync("loginvalue","1")
			        	}else{
							uni.showToast({
								title:res.data.message,
								icon:"none"
							})
						}
					},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style>
	.content {
		background: #3F536E;
		width: 100vw;
		height: 100vh;
	}
	.logodiv{
		width: 100vw;
		height: 30vh;
		display: flex;
		justify-content: center;
		align-items:flex-end;
	}
	.logo{
		width: 200upx;
		height: 200upx;
		overflow: hidden;
	}
	.logo .imglogo{
		width: 100%;
	}
	.form{
		padding: 0 100upx;
		margin-top: 80upx;
	}
	.username{
		width: 100%;
		height: 60upx;
		background: white;
		border-radius: 20upx;
		box-sizing: border-box;
		padding: 0 20upx;
		margin-top: 25upx;		
	}
	.username .nameform{
		width: 100%;
		height: 100%;
		text-align: center;
		font-size: 25upx;
	}
	.password{
		width: 100%;
		height: 60upx;
		background: white;
		border-radius: 20upx;
		box-sizing: border-box;
		padding: 0 20upx;
		margin-top: 25upx;		
	}
	.password .pawform{
		width: 100%;
		height: 100%;
		text-align: center;
		font-size: 25upx;
	}
	.loginBtn{
		width: 100%;
		height: 60upx;
		background: #007cb1;
		border-radius: 50upx;
		margin-top: 50upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.loginBtn .btnvalue{
		color: white;
	}
	.registBtn{
		text-align: center;
		color: #007cb1;
		font-size: 25upx;
		margin-top: 20upx;
	}
	.loginBtnhover{
		background: #3e3e5d;
	}

</style>
