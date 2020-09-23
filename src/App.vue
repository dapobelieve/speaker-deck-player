<template>
	<div class="text-center pb-8">
		<!-- <h3 class="text-4xl">Speaker Deck Slider</h3> -->
		<player />
	</div>
</template>
<script>
export default {
	
	components: {
		Player: () => import("@/app/Player")
	}
}
</script>