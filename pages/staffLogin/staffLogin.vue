<template>
	<view v-if="showAll">
		
		<view class="d-flex flex-column a-center" style="padding-top: 100rpx;padding-bottom: 80rpx;">
			<view class="photo" style="overflow: hidden"><open-data type="userAvatarUrl"></open-data></view>
			<view class="font-30 font-weight mt-2"><open-data type="userNickName"></open-data></view>
		</view>
		<!-- <view class="loginBj pr">
			<image src="../../static/images/the-login-img.png" mode=""></image>
		</view> -->
		
		<view class="loginCont">
			<view class="item d-flex a-center mb-4">
				<view class="icon"><image src="../../static/images/the-loginl-icon.png" mode=""></image></view>
				<view class="input">
					<input type="text" v-model="submitData.login_name" placeholder="请输入登录名" placeholder-class="placeholder">
				</view>
			</view>
			<view class="item d-flex a-center mb-4">
				<view class="icon"><image src="../../static/images/the-loginl-icon1.png" mode=""></image></view>
				<view class="input">
					<input type="password" v-model="submitData.password" placeholder="请输入您的密码" placeholder-class="placeholder">
				</view>
			</view>
			
			<view class="item submitbtn" style="padding:200rpx 0 0 0;border: 0;" >
				<button class="Wbtn" type="submint" @click="submit">登录</button>
			</view>
		</view>
		
		
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				submitData:{
					login_name:'',
					password:''
				},
				showAll:false
			}
		},
		
		onLoad(options) {
			const self = this;
			if (uni.getStorageSync('staff_token')&&uni.getStorageSync('staff_info').user_type==1) {
				uni.redirectTo({
					url: '/pages/staffUser/staffUser'
				})
			}else{
				self.showAll = true
			}
		},
		
		methods: {
			
			submit() {
				const self = this;
			
				const postData = {
					login_name: self.submitData.login_name,
					password:self.submitData.password
				};
				if (self.$Utils.checkComplete(self.submitData)) {
					
					const callback = (res) => {
						if (res.solely_code == 100000) {
							console.log(res);
							uni.setStorageSync('staff_token', res.token);
							uni.setStorageSync('staff_info', res.info);
							uni.redirectTo({
								url: '/pages/staffUser/staffUser'
							}) 
						} else {
							self.$Utils.showToast(res.msg,'none')
						}
					}
					self.$apis.login(postData, callback);
				} else {
					self.$Utils.showToast('请补全登录信息', 'none')
				};
			},
			
		},
	};
</script>

<style>
	
	page{padding-bottom: 60rpx;}	
	.loginBj{width: 440rpx;height: 440rpx;margin: 0 auto;}
	.loginBj image{width: 100%;height: 100%;}
	
	.photo{width: 160rpx;height: 160rpx;border-radius: 50%;overflow: hidden;}
	
	.loginCont{width:90%;margin: 0 auto;z-index: 2;background: #fff;padding: 0rpx 60rpx;box-sizing: border-box;}
	.loginCont .item{height: 80rpx;box-sizing: border-box;padding: 0 20rpx;border-bottom: 1px solid #c3c3c3;}
	.loginCont .item .icon{width: 36rpx;height: 36rpx;margin-right: 30rpx;}
	.loginCont .item .input{width: 85%;}
	.loginCont .item .input input{font-size: 26rpx;height: 60rpx;}
</style>
