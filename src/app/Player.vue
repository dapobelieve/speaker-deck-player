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
					<div @click="slideTo('-')" class="prev">
						<div :class="{'disable': slider.current === 1}" class="material-icons text-white cursor-pointer">
						arrow_back_ios
						</div>
					</div>
					<div @click="slideTo('+')" class="next">
						<div :class="{'disable': slider.current == slider.items.length }" class="material-icons text-white cursor-pointer">
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
			<div class="player-slider  rounded">
				<div v-for="image in images" class="slide-item flex">
					<img class="rounded" :src="image" alt="">
				</div>
			</div>
			<div class="player-tiles bottom-0 left-0 w-full absolute rounded-t-none items-center flex flex-row cursor-pointer">
				<div @click="slider.current = x; slide()" :style="`width: ${computeWidth}%`" v-for="x in slider.items.length" class="tile flex justify-center items-center" :class="{'bg-pink-500': slider.current >= x, 'height-2x': hover}">
					<div ref="preview" :class="{'left': currTileOffsetLeft !==0 && currTileOffsetLeft < (150/2), 'right': currTileOffsetRight < (150/2)}" class="preview absolute" :style="`background-image: url(${images[x-1]})`"></div>
				</div>
			</div>		
		</div>
	</div>
</template>
<script>
export default {
	data () {
		return {
			slider: {
				items: 0,
				current: 1
			},
			hover: false,
			show: 1,
			currTileOffsetLeft: null,
			currTileOffsetRight: null,
			images: [
				'https://res.cloudinary.com/rohing/image/upload/v1585572497/harley-davidson-1HZcJjdtc9g-unsplash_vwslej.jpg',
				'https://avatars2.githubusercontent.com/u/15062380?s=460&u=2f400d9555dc07bc4d2c2d25483ddba570fef29b&v=4',
				'https://res.cloudinary.com/rohing/image/upload/v1587700139/photo-1542393545-10f5cde2c810_zvvwje.jpg'
			]
		}
	},
	computed: {
		computeWidth() {
			return parseFloat(100/this.slider.items.length)
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
		},
		slideTo(sign) {
			if(sign === '+' && this.slider.current != this.slider.items.length) {
				++this.slider.current
			}else if(sign === '-' && this.slider.current != 1) {
				--this.slider.current
			}
			this.slide()
		},
		slide() {
			let slide = this.slider.current
			
			if(this.slider.current < 1) slide = 1
			if(this.slide.current > this.slider.items.length) slide = this.slider.items.length

			for(var i=0; i<this.slider.items.length; i++) {
				this.slider.items[i].style.display = 'none'
			}
			this.slider.items[slide - 1].style.display = 'block'
		}
	},
	mounted() {
		this.slider.items = document.querySelectorAll('.slide-item')
		this.slide()
	}
}
</script>
<style lang="scss">
.player {
	overflow: hidden;
	// width: 400px;
	// height: 400px;

	.player-slider{
		.slide-item {
			height: 600px;

			img {
				height: 100%;
				width: 100%;
				object-fit: cover;
			}
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
			height: 7px;		

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
		background-color: rgba(0, 0, 0, 0.4);
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
		background-color: rgba(0, 0, 0, 0.4);
		padding: 0 10px 15px;
		overflow: hidden;
		height: 70px;
		
		.disable {
			color: #4a544a;
			cursor: default;
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