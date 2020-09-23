<template>
	<div class="container bg-gray-400 mx-auto">
		<player />
	</div>
</template>
<script>
export default {
	components: {
		Player: () => import("@/app/Player")
	},
	mounted() {
		console.log("APP LOADED")
	}
}
</script>
<style lang="scss">

</style>