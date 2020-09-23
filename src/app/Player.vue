<template>
	<div class="container mx-auto mt-3">
		<div class="player relative bg-white rounded" @mouseover="hover = true" @mouseleave="hover = false">
			<div class="player-info top-0 flex flex-row w-full items-center rounded-t absolute px-4">
					<div class="avatar mr-5">
						<img src="https://avatars2.githubusercontent.com/u/15062380?s=460&u=2f400d9555dc07bc4d2c2d25483ddba570fef29b&v=4" alt="">
					</div>
					<div class="title flex flex-col">
						<h3 class="font-bold text-lg text-white">How to build a speaker deck player</h3>
						<span class="text-left text-sm">by: <span class="font-bold">King Believe</span></span>
					</div>
			</div>
			<div class="player-controls flex items-end absolute bottom-0 right-0 left-0 bg-yellow-200">
				<div class="prev">
					<div class="material-icons text-white cursor-pointer">
					arrow_back_ios
					</div>
				</div>
				<div class="next">
					<div class="material-icons text-white cursor-pointer">
						arrow_forward_ios
					</div>
				</div>
				<div class="ml-auto">
					<div class="material-icons text-white cursor-pointer">
					present_to_all
					</div>
				</div>		
			</div>
			<div class="player-slider rounded">
				<img class="rounded" :src="images[0]" alt="">
			</div>
			<div v-if="show" class="player-tiles bottom-0 left-0 w-full absolute rounded-t-none  cursor-pointer">
				<div class="tile"></div>
			</div>		
			<!-- show-controls -->
		</div>
	</div>
</template>
<script>
export default {
	data () {
		return {
			hover: false,
			show: 2,
			images: [
				'https://res.cloudinary.com/rohing/image/upload/v1585572497/harley-davidson-1HZcJjdtc9g-unsplash_vwslej.jpg',
				'https://avatars2.githubusercontent.com/u/15062380?s=460&u=2f400d9555dc07bc4d2c2d25483ddba570fef29b&v=4'
			]
		}
	},
}
</script>
<style lang="scss">
.player {
	overflow: hidden;
	.player-slider{
		height: 600px;

		img {
			height: 100%;
			width: 100%;
			object-fit: cover;
		}
	}

	.player-tiles {
		background-color: #009287;
		height: 5px;
		width: 27.8%
	}

	.player-info {
		background-color: rgba(0, 0, 0, 0.5);
		height: 70px;
		transform: translateY(-70px);

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
		background-color: rgba(0, 0, 0, 0.5);
		padding: 0 10px 15px;
		// transform: translateY(72px);
		overflow: hidden;
		height: 70px;
		transition: transform 0.3s ease, -webkit-transform 0.3s ease;

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

}	
</style>