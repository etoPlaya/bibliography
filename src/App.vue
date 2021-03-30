<template>
  <div id="app">
    <TheHeader/>
    
    <main>
      <div class="container">
        <Libary/>
        <Collection/>
      </div>
    </main>
  </div>
</template>

<script>
import TheHeader from '@/components/TheHeader';
import Libary from '@/components/Libary';
import Collection from '@/components/Collection';

export default {
  name: 'App',
  components: {
    TheHeader,
    Libary,
    Collection,
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
