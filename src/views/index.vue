<template>
	<div id="index">
		<dv-full-screen-container class="bg">
			<dv-loading v-if="loading">Loading...</dv-loading>
			<div v-else class="host-body">
				<div style="" class="topdiv">
	
					<div class="titletext">
						Big Herdsman 大牧人 丨 福建圣农集团
					</div>
					<div class="topbg">
						<img :src="leftBg" alt="">
						<img :src="rightBg" alt="">
					</div>
					<div class="login">
					</div>
				
				</div>
				<div class="linebox">

				</div>
		

				<div class="body-box">
					<!-- 左侧图表数据 -->
					<div class="content-box">
						<div>
							<div class="leftbox">
								<div class="leftbox-one">
									<div class="title-top">
										<img :src="adminIcon" alt="">
										集团存栏量
									</div>
									<div class="selectbox">
										<div @click="selectbox(1)" :class="[active==1?'active':'']"><span>柱</span></div>
										<div @click="selectbox(2)" :class="[active==2?'active':'']"><span>饼</span></div>
									</div>
									<centerLeft3 v-show="active==1" />
									<centerLeft1 v-show="active==2" />
									
									<div class="dot">
										<span v-for="item in dot" :class="[item==2?'active':'']" :key="item"></span>
									</div>
								</div>
								<div class="leftbox-one">
									<div class="title-top">
										<img :src="adminIcon2" alt="">
										场区存栏量
									</div>
									<centerRight1 v-show="false" />
									<div class="leftbottombox">
										<div class="lbb-line">
											<div style="text-align: right;">
												XX XX场
											</div>
										</div>
										<div class="lbb-line">
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
										</div>
										<div class="lbb-line">
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
											<div>
												XX XX场
											</div>
										</div>
									</div>
								</div>
								<div class="border1"></div>
								<div class="border2"></div>
								<div class="border3"></div>
								<div class="border4"></div>
							</div>
						</div>
						<div>
							<div class="centerbox">
								<div class="centertitle">
									<div class="titlebox" v-for="(item,index) in titleList" :key="index">
										<div class="titlename">{{item.name}}</div>
										<div class="titlenum">{{item.num}}<span>{{item.code}}</span></div>
									</div>
								</div>
								<div class="centerbox-map">
                  <!-- 地图数据 -->
									<centerLeft2 />
									<div class="centerbottom">
										<div>场区总览</div>
										<div>查看报警</div>
										<div>当前报警：XX场XX舍XX报警 已处理</div>
									</div>
								</div>
							</div>
						</div>

						<div>
							<!-- 右侧图表-->
							<div class="leftbox">
								<div class="leftbox-one">
									<div class="title-top">
										<img :src="adminIcon" alt="">
										温湿度
									</div>
									<bottomRight />
									<div class="dot">
										<span v-for="item in dot" :class="[item==2?'active':'']" :key="item"></span>
									</div>
								</div>
								<div class="leftbox-one">
									<div class="selectbox">
										<div @click="selectbox1(1)" :class="[active1==1?'active':'']"><span>柱</span></div>
										<div @click="selectbox1(2)" :class="[active1==2?'active':'']"><span>饼</span></div>
									</div>
									<div class="title-top">
										<img :src="adminIcon3" alt="">
										报警信息
									</div>
									<centerRight2 v-show="active1==1"/>
                  <centerLeft1 v-show="active1==2" />
									<div class="dot">
										<span v-for="item in dot" :class="[item==2?'active':'']" :key="item"></span>
									</div>
								</div>
								<div class="border1"></div>
								<div class="border2"></div>
								<div class="border3"></div>
								<div class="border4"></div>
							</div>
						</div>
						<div>
						</div>
					</div>

				</div>
			</div>
		</dv-full-screen-container>
	</div>
</template>

<script>
	import {
		formatTime
	} from '../utils/index.js'
	import centerLeft1 from "./centerLeft1";  // 左侧图表 环图
	import centerLeft2 from "./centerLeft2";  // 中心地图
	import centerLeft3 from "./centerLeft3"; // 左侧图表 柱状图
	import centerRight1 from "./centerRight1"; // 
	import centerRight2 from "./centerRight2"; // 右侧 柱状图
	// import centerRight3 from "./centerRight3"; // 右侧 环形图
	import bottomRight from "./bottomRight"; // 右侧则线图
	export default {
		data() {
			return {
				dot: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11],
				active: 1,
				active1: 1,
				titleBg: require('../assets/titleBg.png'),
				leftBg: require('../assets/left.png'),
				rightBg: require('../assets/right.png'),
				adminIcon: require('../assets/4.svg'),
				adminIcon2: require('../assets/2.svg'),
				adminIcon3: require('../assets/1.svg'),
				loading: true,
				dateDay: null,
				dateYear: null,
				dateWeek: null,
				weekday: ["周日", "周一", "周二", "周三", "周四", "周五", "周六"],
				titleList: [{
					name: '当前在线',
					num: '15',
					code: '场'
				}, {
					name: '当前离线',
					num: '05',
					code: '场'
				}, {
					name: '未处理报警',
					num: '09',
					code: '个'
				}, {
					name: '今日报警数',
					num: '20',
					code: '个'
				}]
			};
		},
		components: {
			centerLeft1,
			centerLeft3, // 切换
			centerLeft2,
			centerRight1,
			centerRight2,
			// centerRight3,
			bottomRight
		},
		mounted() {
			this.timeFn();
			this.cancelLoading();
		},
		methods: {
			selectbox(index) {
				this.active = index;
			},
			selectbox1(index) {
				this.active1 = index;
			},
			timeFn() {
				setInterval(() => {
					this.dateDay = formatTime(new Date(), 'HH: mm: ss');
					this.dateYear = formatTime(new Date(), 'yyyy-MM-dd');
					this.dateWeek = this.weekday[new Date().getDay()];
				}, 1000)
			},
			cancelLoading() {
				setTimeout(() => {
					this.loading = false;
				}, 500);
			}
		}
	};
</script>

<style lang="scss">
	@import '../assets/scss/index.scss';

	.bg {
		padding: 0 !important;
	}

	// 头部背景
	.topdiv {
		height: 1rem;
		width: 100%;
		background-image: linear-gradient(to right, #1b172e, #294473, #1b172e);
		.lefttext {
			color: #658ea3;
			font-size: 0.24rem;
			top: 0.38rem;
			line-height: 0.24rem;
			position: absolute;
			left: 0.6rem;
		}

		.topselect {
			color: rgba(255, 255, 255, .7);
			border: 1px solid rgba(255, 255, 255, .5);
			height: 0.5rem;
			box-sizing: content-box;
			border-radius: 0.04rem;
			width: 2rem;
			line-height: 0.5rem;
			padding-left: 0.2rem;
			position: absolute;
			left: 2.5rem;
			top: 0.25rem;
			cursor: pointer;

			&:after {
				content: "";
				position: absolute;
				bottom: 0.2rem;
				right: 0.3rem;
				transform: rotate(45deg);
				-webkit-transform: rotate(45deg);
				border: solid #fff;
				border-width: 0 1px 1px 0;
				display: inline-block;
				padding: 3px;
			}
		}

		.titleBg {
			height: 1rem;
			width: 100%;
		}

		.titletext {
			font-size: 0.4rem;
			line-height: 1rem;
			color: #fff;
			position: absolute;
			width: 100%;
			text-align: center;
			left: 0;
			top: 0;
		}

		.login {
			top: 0.35rem;
			font-size: 0.24rem;
			line-height: 0.3rem;
			height: 0.3rem;
			width: 1rem;
			position: absolute;
			padding-left: 0.4rem;
			right: 3.6rem;

			div {
				position: absolute;
				left: 0;
				height: 0.24rem;
				width: 0.24rem;
				border-radius: 50%;
				background: #02c9ff;
				top: 0;
			}
		}

		.out {
			top: 0.35rem;
			font-size: 0.24rem;
			line-height: 0.3rem;
			height: 0.3rem;
			width: 1rem;
			position: absolute;
			padding-left: 0.4rem;
			right: 2.5rem;

			img {
				position: absolute;
				left: 0;
				height: 0.24rem;
				width: 0.24rem;
				top: 0;
			}
		}

		// 管理员
		.admin {
			top: 0.3rem;
			font-size: 0.3rem;
			line-height: 0.4rem;
			height: 0.4rem;
			width: 2rem;
			position: absolute;
			padding-left: 0.5rem;
			right: 0;

			img {
				position: absolute;
				left: 0;
				height: 0.4rem;
				width: 0.4rem;
				top: 0;
			}
		}
	}

	.linebox {
		height: 0.1px;
		background-image: linear-gradient(to right, #2f4459, #6098f7, #2f4459);
	}

	.leftbox {
		.selectbox {
			z-index: 999;
			width: 1.2rem;
			height: 0.25rem;
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: flex-start;
			position: absolute;
			right: 0.2rem;
			top: 0.25rem;

			div {
				flex: 1;
				background: #1b172e;
				text-align: center;
				color: #fff;
				font-size: 0.12rem;
				cursor: pointer;
				line-height: 0.25rem;

				span {
					transform: scale(0.8)
				}

				&.active {
					background: #6665fd;
				}
			}

		}

		height: 11.4rem;
		// margin-left: 40px;
		// width: 440px;
		padding:0px 0.25rem 0;
		margin-top: 0.6rem;
		position: relative;

		.leftbox-one {
			.leftbottombox{
				padding: 0.5rem;
				padding-bottom: 0;
				.lbb-line{
					display: flex;
					flex-direction: row;
					align-items: center;
					justify-content: flex-end;
					padding: 0.2rem;
					border-bottom: 1px solid #4c4d69;
					flex-wrap: wrap;
					div{
						width: 50%;
						line-height: 0.6rem;
						height: 0.6rem;
						font-size: 0.2rem;
					}
					div:nth-child(2n){
						text-align: right;
					}
				}
			}
			.dot {
				display: flex;
				flex-direction: row;
				justify-content: center;
				position: absolute;
				align-items: center;
				bottom: 0.2rem;
				width: 100%;

				span {
					margin: 0 0.14rem;
					display: inline-block;
					height: 0.06rem;
					background: #fff;
					width: 0.06rem;
					border-radius: 50%;

					&.active {
						height: 0.08rem;
						width: 0.08rem;
						background: #d85a25;
					}
				}
			}

			border-radius: 0.1rem;
			overflow: hidden;
			// width: 420px;
			height: 5.5rem;
			background: #272441;

			&:nth-child(1) {
				margin-bottom: 0.4rem;
			}

			position: relative;

			.title-top {
				position: absolute;
				left: 0.2rem;
				top: 0.25rem;
				padding-bottom: 0.02rem;
				display: flex;
				flex-direction: row;
				justify-content: flex-start;
				align-items: center;
				font-size: 0.22rem;
				color: #fff;
				border-bottom: 2px solid #bf4b10;

				img {
					margin-right: 0.1rem;
					width: 0.2rem;
					height: 0.2rem;
					display: block;
				}
			}
		}

		.border1 {
			width: 0.6rem;
			height: 0.6rem;
			border: 2px solid #8aa8f6;
			border-right: none;
			border-bottom: none;
			position: absolute;
			left: 0.1rem;
			top: -0.2rem;
		}

		.border2 {
			width: 0.6rem;
			height: 0.6rem;
			border: 2px solid #8aa8f6;
			border-left: none;
			border-bottom: none;
			position: absolute;
			right: 0.1rem;
			top: -0.2rem;
		}

		.border3 {
			width: 0.6rem;
			height: 0.6rem;
			border: 2px solid #8aa8f6;
			border-right: none;
			border-top: none;
			position: absolute;
			left: 0.1rem;
			bottom: -0.2rem;
		}

		.border4 {
			width: 0.6rem;
			height: 0.6rem;
			border: 2px solid #8aa8f6;
			border-left: none;
			border-top: none;
			position: absolute;
			right: 0.1rem;
			bottom: -0.2rem;
		}
	}

	.centerbox {
		position: relative;

		.centerbox-map {
			height: 10rem;
			position: relative;
			overflow: hidden;
		}

		.centerbottom {
			bottom: 0;
			position: absolute;
			right: 0.4rem;
			display: flex;
			flex-direction: column;
			align-items: flex-end;
			width: auto;

			div {
				height: 0.6rem;
				width: auto;
				box-sizing: content-box;
				line-height: 0.6rem;
				margin-bottom: 0.5rem;
				padding: 0 0.4rem;
				border: 1px solid #fff;
				border-radius: 4px;
				color: #00e8ff;
				background: #292643;
			}
		}

		.centertitle {
			display: flex;
			height: 1.5rem;
			padding-top: 0.4rem;
			box-sizing: content-box;
			flex-direction: row;
			align-items: center;
			justify-content: center;

			.titlebox {
				width: 2.4rem;
				height: 1.5rem;
				text-align: center;

				.titlename {
					height: 0.34rem;
					font-size: 0.34rem;
					color: #829de3;
					margin-bottom: 0.22rem;
				}

				.titlenum {
					height: 0.5rem;
					font-size: 0.5rem;
					font-weight: 700;

					span {
						display: inline-block;
						margin-left: 0.05rem;
						font-weight: 400;
						font-size: 0.22rem;
						color: rgba(255, 255, 255, .5);
					}
				}
			}
		}
	}
	.topbg{
		height: 1rem;
		width: 100%;
		position: absolute;
		top: 0;
		left: 0;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		img{
			margin: 0 4.2rem;
			width: 3rem;
			height: 0.4rem;
			object-fit: cover;
		}
	}
</style>
