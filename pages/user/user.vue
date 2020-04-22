<template>
	<view class="content">
		<view class="logodiv">
			<view class="logo">
				<image class="imglogo" src="../../static/logo.png" mode="widthFix"></image>
			</view>
		</view>
		<view class="form">
			<view class="loginBtn" hover-class="loginBtnhover">
				<view v-if="aa==='1'">
					<text class="btnvalue" @tap="cleanlogin">注销登录</text>
				</view>
				<view v-else>
					<navigator url="../login/login" class="btnvalue">登录</navigator>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				aa:uni.getStorageSync("loginvalue")
			}
		},
		onPullDownRefresh(){
			setTimeout(()=>{
				 this.$forceUpdate() 
				uni.stopPullDownRefresh()
			},2000)
		},
		methods:{
			cleanlogin(){
				uni.showToast({
					title:"注销成功",
					icon:"none"
				});
				uni.removeStorageSync("loginvalue");
			    uni.reLaunch({
			    	url:"./user"
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
</style>
