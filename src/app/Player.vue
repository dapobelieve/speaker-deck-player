<template>
	<div class="container mx-auto mt-3">
		<div ref="player" class="player relative bg-white rounded" @mouseover="computeHover($event)" @mouseleave="hover = false">
			<transition name="slidedown">
				<div v-if="hover" class="player-info top-0 flex flex-row w-full items-center rounded-t absolute px-4">
					<div class="avatar mr-5">
						<img src="https://avatars2.githubusercontent.com/u/15062380?s=460&u=2f400d9555dc07bc4d2c2d25483ddba570fef29b&v=4" alt="">
					</div>
					<div class="title flex flex-col">
						<h3 class="font-bold text-lg text-white">How to build a speaker deck player</h3>
						<span class="text-left text-sm">by: <span class="font-bold text-white">King Believe</span></span>
					</div>
				</div>
			</transition>
			<transition name="slideup">
				<div v-if="hover" class="player-controls flex items-end absolute bottom-0 right-0 left-0 bg-yellow-200">
					<div @click="show--" class="prev">
						<div class="material-icons text-white cursor-pointer">
						arrow_back_ios
						</div>
					</div>
					<div class="next">
						<div @click="show++" disable class="material-icons text-white cursor-pointer">
							arrow_forward_ios
						</div>
					</div>
					<div class="ml-auto">
						<div class="material-icons text-3xl text-white cursor-pointer">
						present_to_all
						</div>
					</div>		
				</div>
			</transition>
			<div class="player-slider flex rounded">
				<img class="rounded" :src="images[0]" alt="">
			</div>
			<div class="player-tiles bottom-0 left-0 w-full absolute rounded-t-none items-center flex flex-row cursor-pointer">
				<div @click="show = x" :style="`width: ${computeWidth}%`" v-for="x in numberOfSlides" class="tile flex justify-center items-center" :class="{'bg-pink-500': show >= x, 'height-2x': hover}">
					<div ref="preview" :class="{'left': currTileOffsetLeft < (150/2), 'right': currTileOffsetRight < (150/2)}" class="preview absolute" :style="`background-image: url(${images[1]})`"></div>
				</div>
			</div>		
		</div>
	</div>
</template>
<script>
export default {
	data () {
		return {
			hover: true,
			numberOfSlides: 20,
			show: 3,
			currTileOffsetLeft: null,
			currTileOffsetRight: null,
			images: [
				'https://res.cloudinary.com/rohing/image/upload/v1585572497/harley-davidson-1HZcJjdtc9g-unsplash_vwslej.jpg',
				'https://avatars2.githubusercontent.com/u/15062380?s=460&u=2f400d9555dc07bc4d2c2d25483ddba570fef29b&v=4'
			]
		}
	},
	computed: {
		computeWidth() {
			return parseFloat(100/this.numberOfSlides)
		},
		playerWidth() {
			return this.$refs['player'].offsetWidth
		}
	},
	methods: {
		computeHover(e) {
			this.hover = true;

			if(Object.values(e.target.classList).includes('tile')) {
				this.currTileOffsetLeft = e.target.offsetLeft
				this.currTileOffsetRight = this.playerWidth - this.currTileOffsetLeft

				e.target.parentNode.classList.toggle('height-2x')
			}
		}
	}
}
</script>
<style lang="scss">
.player {
	overflow: hidden;
	// width: 400px;
	// height: 400px;

	.player-slider{
		height: 600px;

		img {
			height: 100%;
			width: 100%;
			object-fit: cover;
		}
	}

	.player-tiles {
		&.height-2x {
			height: 10px;
			div {
				height: 10px
			}
		}
		
		.tile {
			height: 5px;		

			&:hover .preview {
				display: block;
			}

			.preview {
				display: none;
				bottom: 30px;
				height: 80px;
				width: 150px;
				background-position: center;
				background-size: cover;
				background-repeat: no-repeat;
				border-radius: 4px;

				&.left {
					left: 5px
				}
				&.right {
					right: 10px
				}
			}
		}
	}

	.player-info {
		background-color: rgba(0, 0, 0, 0.5);
		height: 70px;
		
		.avatar {
			height: 40px;
			width: 40px;

			img {
				height: 100%;
				width: 100%;
				object-fit: cover;
				border-radius: 50%
			}
		}
	}

	.player-controls {
		background-color: rgba(0, 0, 0, 0.9);
		padding: 0 10px 15px;
		overflow: hidden;
		height: 70px;
		

		.prev {
			::before {
				content: '';
				position: absolute;
				background-color: red;
				top: 0;
				right: 50%
			}
		}
	}

	.slidedown-enter-active, .slidedown-leave-active, .slideup-enter-active, .slideup-leave-active {
		transition: transform 0.3s ease, -webkit-transform 0.3s ease;
	}

	.slidedown-enter, .slidedown-leave-to {
		transform: translateY(-70px);
	}

	.slideup-enter, .slideup-leave-to {
		transform: translateY(72px);
	}
}	
</style>