
<script>
	import token from "./common/token.js"
	export default {
		onLaunch: function() {	
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/* @import "/assets/style/style.css"; */
	/* 动画样式 */
	@import "/common/css/animate.css";
	@import "/common/css/swiper.min.css";
	
	@import "/assets/style/quill.css";
	/* 公共样式 */
	@import "/common/css/common.css";
	/* 公共样式 */
	@import "/common/css/main.css";
	
	uni-swiper .uni-swiper-dots-horizontal{line-height: 16rpx;bottom: 5px;}
	
	uni-tabbar .uni-tabbar__icon{width: 44rpx;height: 44rpx;}
	uni-page-head .uni-page-head__title{font-weight: normal;}
	uni-swiper .uni-swiper-dot{background-color: #fff;}
	/* uni-swiper .uni-swiper-dot-active{width: 20rpx;} */
	.ql-editor img{max-width: 100%;margin: 0 auto;}
	.uni-page-head{border-bottom: 1px solid #eee;}
</style>
