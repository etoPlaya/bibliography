<template>
	<section>

	</section>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

	section {
		max-width: 950px;
		width: 100%;

		height: calc(100% - 69px);
		height: calc(100vh - 69px);

		padding: 20px 40px;
		@media (min-width: 1200px) and (max-height: 768px) {
			height: auto;
		}
		@media screen and (max-width: 768px) {
			height: auto;
		}
	}
</style>