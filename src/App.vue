<template>
  <div id="app">
		<customHeader/>
		<main>
			<div class="container">
				<libary/>
				<selectLibary/>
			</div>
		</main>
  </div>
</template>

<script>

import customHeader from '@/components/customHeader';
import libary from '@/components/libary';
import selectLibary from '@/components/selectLibary';

export default {
  name: 'App',
  components: {
		customHeader,
		libary,
		selectLibary,
  }
}

</script>

<style lang="scss">

@import url('https://necolas.github.io/normalize.css/8.0.1/normalize.css');
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
@import '@/styles/default.scss';
@import '@/styles/fonts.scss';

#app {
	font-family: "PT Root UI";
	color: $default;
	background-color: $brand;
	.content {
		position: relative;
		padding: 12px 40px;
	}
	main {
		.container {
			display: flex;
			justify-content: space-between;
			align-items: flex-start;
		}
	}
}

body {
	background-color: $brand;
}

</style>
