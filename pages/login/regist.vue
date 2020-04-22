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
			<view class="name">
				<input class="name" type="text" v-model="realname" placeholder="请输入姓名" />
			</view>
			<view class="password">
				<input class="pawform" type="password" v-model="password" placeholder="请输入密码" />
			</view>
			<view class="passwordup">
				<input class="pawformup" type="password" v-model="checkword" placeholder="请再次输入密码" />
			</view>
			<view class="registBtn" hover-class="registBtnhover" @tap="loginrequest">
				<text class="btnvalue">注册</text>
			</view>
			<view class="loginBtn">
				<navigator url="./login" class="login" open-type="redirect">返回登陆</navigator>
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
				name:'',
				checkword:''
			}
		},
		methods: {
			loginrequest(){
				uni.request({
					url: 'http://127.0.0.1:8088/robot/user/regist',
					method: 'POST',
					data: {
						username:this.username,
						password:this.password,
						realname:this.realname,
						checkword:this.checkword
					},
					header:{
						"content-type":"application/x-www-form-urlencoded"
					},
					success: res => {
						uni.showToast({
							title:res.data.message,
							icon:"none"
						})
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
	.name{
		width: 100%;
		height: 60upx;
		background: white;
		border-radius: 20upx;
		box-sizing: border-box;
		padding: 0 20upx;
		margin-top: 25upx;		
	}
	.name .name{
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
	.passwordup{
		width: 100%;
		height: 60upx;
		background: white;
		border-radius: 20upx;
		box-sizing: border-box;
		padding: 0 20upx;
		margin-top: 25upx;		
	}
	.passwordup .pawformup{
		width: 100%;
		height: 100%;
		text-align: center;
		font-size: 25upx;
	}
	.registBtn{
		width: 100%;
		height: 60upx;
		background: #007cb1;
		border-radius: 50upx;
		margin-top: 50upx;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.registBtn .btnvalue{
		color: white;
	}
	.loginBtn{
		text-align: center;
		color: #007cb1;
		font-size: 25upx;
		margin-top: 20upx;
	}
	.registBtnhover{
		  position: relative;
		  top: 3rpx;
		  left: 3rpx;
		  box-shadow:0px 0px 8px rgba(0,0,0,.1) inset; 
	}
</style>
