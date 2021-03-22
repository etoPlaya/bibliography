<template>
  <div id="app">
		<customHeader></customHeader>
		<main>
			
		</main>
  </div>
</template>

<script>

import customHeader from '@/components/customHeader';

export default {
  name: 'App',
  components: {
		customHeader
  }
}
</script>

<style lang="scss">
@import url('https://necolas.github.io/normalize.css/8.0.1/normalize.css');
@import './styles/mixin.scss';
@import './styles/variable.scss';
@import './styles/default.scss';
@import './styles/fonts.scss';
#app {
	font-family: "PT Root UI";
	color: $default;
	background-color: $brand;
	.content {
		position: relative;
		padding: 12px 40px;
	}
}
body {
	background-color: $brand;
}
</style>
