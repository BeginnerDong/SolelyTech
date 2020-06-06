<template>
	<view>
		
		<view class="homeHead">
			<view class="banner-box">
				<image src="../../static/images/banner-img.png" mode=""></image>
				
				<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="4000" duration="0" @change="this.current">
					<block>
						<swiper-item class="swiper-item position-relative overflow-h">
							<image src="../../static/images/banner-txt2.png" class="banner-img1 banner-img" :animation="animationData"/>
							<image src="../../static/images/banner-img1.png" class="banner-img2 banner-img" :animation="animationData2"/>
						</swiper-item>
					</block>
					<block>
						<swiper-item class="swiper-item position-relative">
							<image src="../../static/images/banner-txt1.png" class="banner-img1 banner-img" :animation="animationData"/>
							<image src="../../static/images/banner-img2.png" class="banner-img2 banner-img" :animation="animationData2"/>
						</swiper-item>
					</block>
				</swiper>
			</view>
		</view>
		
		<view class=" d-flex j-sb a-center homeNav">
			<view class="half d-flex j-center a-center">
				<view class="item d-flex flex-column a-center" @click="Router.navigateTo({route:{path:'/pages/hotjob/hotjob'}})">
					<view class="icon"><image src="../../static/images/home-icon.png" mode=""></image></view>
					<view class="tit mt-2" style="color: #9087f9;">热招职位</view>
					<view class="text">期待加入</view>
				</view>
			</view>
			<view class="half rr">
				<view class="item d-flex a-center" @click="intoMap">
					<view class="icon"><image src="../../static/images/home-icon1.png" mode=""></image></view>
					<view>
						<view class="tit"  style="color: #5cdfdd;">一键导航</view>
						<view class="text">期待到来</view>
					</view>
				</view>
				<view class="item d-flex a-center" @click="Router.navigateTo({route:{path:'/pages/contactUs/contactUs'}})">
					<view class="icon"><image src="../../static/images/home-icon2.png" mode=""></image></view>
					<view>
						<view class="tit" style="color: #ff79fd;">联系我们</view>
						<view class="text">为您服务</view>
					</view>
				</view>
			</view>
		</view>
		<view class="f5Bj-H10"></view>
		
		<view class="px-2">
			<view class="Big-title font-30 pt-4 font-weight">西安纯粹云信息科技有限公司</view>
			<view class="d-flex a-center mt-1 flex-wrap">
				<view class="starBox mr-1 mt">
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
				</view>
				<view class="font-22">小程序、公众号、网站、APP开发、LOGO设计</view>
			</view>
			<view class="d-flex j-sb a-center pt-5 mt-1 pb-5 text-center dataList">
				<view class="item">
					<view class="font-40 font-weight">2016</view>
					<view class="mt-2 font-24 color6">开始于</view>
				</view>
				<view class="item">
					<view class="font-40 font-weight">860+</view>
					<view class="mt-2 font-24 color6">服务于</view>
				</view>
				<view class="item">
					<view class="font-40 font-weight">560+</view>
					<view class="mt-2 font-24 color6">在线项目</view>
				</view>
			</view>
			
			<view class="font-26" style="line-height: 50rpx;">纯粹科技创世至今，以雄厚的技术团队和专业的设计团队，帮助中小企业快速搭建移动互联网平台，公司自立于互联网的大环境下，致力于拓新型营销模式，用心打造值得信赖的多元化移动互联网机构。成为中小型企业在移动互联网领域最为信任的合作伙伴，可提供多个行业的解决方案，助力企业实现品牌树立，形象塑造，营销推广等。</view>
			<view class="w-100 pt-4"><image src="../../static/images/home-img2.png" mode="widthFix"></image></view>
		</view>
		
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/caseList/caseList'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">行业案例</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/newsCenter/newsCenter'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">资讯中心</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar4.png" />
				</view>
				<view class="text">个人中心</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				animationData: {},
				animationData2: {},
				index: 0,
				bannerData:[{
					imgOne:'',
					imgTwo:'',
					animation:{}
				},{
					imgOne:'',
					imgTwo:'',
					animation:{}
				}]
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
			
			self.animation = uni.createAnimation()  
			self.running();
		},
		
		onUnload(){
			const self = this;
			self.animationData = {}
			self.animationData2 = {}
		},
		
		methods: {
			// 轮播内容动画
			running() {
				const self = this;
				const { windowWidth } = uni.getSystemInfoSync();
				var x = 0,y = 0;
				if(windowWidth <= 320){x = 280,y = 100}else if(windowWidth <= 375){x = 330,y = 105}else if(windowWidth <=414){x = 350,y = 115}else if(windowWidth == 480){x = 420,y = 150}else if(windowWidth <= 768){x = 670,y = 238}else if(windowWidth <= 834){x = 700,y = 238}else if(windowWidth <= 1024){x = 900,y = 300}
		    
				this.animation.translateX(-x).opacity(0).step({duration:100})
				this.animationData = this.animation.export()
				this.animation.translateX(y).opacity(0).step({duration:100})
				this.animationData2 = this.animation.export();
				
				setTimeout(()=>{
					self.animation.translateX(x).opacity(1).step({duration:500})
					self.animationData = self.animation.export()
					self.animation.translateX(-y).opacity(1).step({duration:500})
					self.animationData2 = self.animation.export()   // export方法导出动画数据
				}, 100);
				
		  },
			current(e){
				const self = this;
				if(e.target.current != this.index){
					this.running();
				}
				this.index = e.target.current;
			},
			
			getMainData(){
			    var self = this;
			    var postData = {};
				postData.tokenFuncName = 'getProjectToken';
			    postData.searchItem = {
					thirdapp_id:2
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData  = res.info.data[0];
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.userInfoGet(postData, callback);
			},
			
			intoMap(){
			  const self = this;
			  wx.getLocation({
			    type: 'wgs84', //返回可以用于wx.openLocation的经纬度
			    success: function (res) {  //因为这里得到的是你当前位置的经纬度
			      var latitude = res.latitude
			      var longitude = res.longitude
			      wx.openLocation({        //所以这里会显示你当前的位置
			        longitude: 108.8939050000,
			        latitude: 34.2377310000,
			        //109.045249,34.325841
			        name: "西安纯粹信息科技有限公司",
			        address:"西安纯粹信息科技有限公司",
			        scale: 28
			      })
			    }
			  })
			},
			
		}
	};
</script>

<style>
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/star.css";
	
	page{padding-bottom: 140rpx;}	
	
	.banner-box{width: 100%;height: 500rpx;position: relative;}
	.swiper-box{position: absolute;top: 0;left: 0;width: 100%;height: 100%;}
	.banner-img{position: absolute;}
	.banner-img1{width: 630rpx;height: 65%;left: -600rpx;top: 70rpx;opacity: 0;}
	.banner-img3{width: 630rpx;height: 65%;left: 30rpx;top: 70rpx;}
	.banner-img2{width: 180rpx;height: 180rpx;right: -180rpx;bottom: 30rpx;opacity: 0;}
	
	.homeNav .half{width: 50%;height: 300rpx;box-sizing: border-box;}
	.homeNav .half:first-child{border-right: 1px solid #eee;}
	.homeNav .half .item{ box-sizing: border-box;padding: 30rpx;}
	.homeNav .half .item .icon{width: 90rpx;height: 90rpx;border-radius: 50%;}
	.homeNav .half.rr .item{width: 100%;height: 150rpx; box-sizing: border-box;}
	.homeNav .half.rr .item:first-child{border-bottom: 1px solid #eee;}
	.homeNav .half.rr .icon{margin-right: 20rpx;}
	.homeNav .half .tit{font-weight: bold;font-size: 30rpx;}
	.homeNav .half .text{font-size: 24rpx;color: #666;}
	
	.dataList .item{width: 33.33%;}
</style>
