<template>
  <div id="app">
    <TheHeader/>
    
    <main>
      <div class="container">
        <Libary 
          :class="{libary_mobile: isMobile}"
        />

        <Collection 
          :class="{hidden: isMobile, collection_mobile: isMobile}"
        />

        <div class="mobile-switch libary" v-if="isMobile">
          <div class="mobile-switch-selected"></div>

          <a href="" class="mobile-switch-button select-libary" @click.prevent="selectLibary">Каталог</a>

          <a href="" class="mobile-switch-button select-collection" @click.prevent="selectCollection">Моя литература</a>
        </div>
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
  },

  data() {
    return {
      catalog: true,
      isMobile: false,
    }
  },

  mounted() {
    this.checkWindowSize();

    window.addEventListener('resize', this.checkWindowSize, { passive: true });
  },

  methods: {
    checkWindowSize() {
      this.isMobile = window.innerWidth < 1100;
    },

    selectLibary() {
      const mobileSwitch = document.querySelector('.mobile-switch');
      const libary = document.querySelector('.libary_mobile');
      const collection = document.querySelector('.collection_mobile');

      if(mobileSwitch.classList.contains('collection')) {
        mobileSwitch.classList.remove('collection');
      }

      mobileSwitch.classList.add('libary');
      libary.classList.remove('hidden');
      collection.classList.add('hidden');
    },

    selectCollection() {
      const mobileSwitch = document.querySelector('.mobile-switch');
      const collection = document.querySelector('.collection_mobile');
      const libary = document.querySelector('.libary_mobile');

      if(mobileSwitch.classList.contains('libary')) {
        mobileSwitch.classList.remove('libary');
      }

      mobileSwitch.classList.add('collection');
      collection.classList.remove('hidden');
      libary.classList.add('hidden');
    },
  },
}
</script>

<style lang="scss">
@import url('https://necolas.github.io/normalize.css/8.0.1/normalize.css');
@import '@/styles/default.scss';
@import '@/styles/fonts.scss';

@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

body {
  background-color: $brand;
  overflow: hidden;

  @include mobile {
    overflow: visible;
  }
}

#app {
  font-family: "PT Root UI", sans-serif;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  color: $default;
  background-color: $brand;

  .content {
    position: relative;
    padding: 12px 40px;
  }

  main {
    flex: 1;
    min-height: 100%;
    height: 1px; /* Требуется, чтобы дочерний блок взял высоту 100% */

    .container {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      
      height: 100%;

      .mobile-switch {
        display: flex;
        align-items: center;
        
        position: fixed;
        bottom: 20px;
        left: 0;
        right: 0;

        max-width: 240px;
        width: 100%;
        min-height: 44px;

        background: #686D92;
        box-shadow: 0px 4px 16px rgba(45, 47, 68, 0.24);
        border-radius: 26px;

        margin: 0 auto;
        padding: 4px;

        z-index: 9999;

        $root: &;

        &-button {
          position: relative;
          
          display: block;
          width: 50%;
          
          font-size: 13px;
          line-height: 16px;
          font-weight: bold;
          text-align: center;
          color: #FFFFFF;

          transition: 250ms linear all;
        }

        &-selected {
          position: absolute;
          left: 4px;
          
          width: calc(50% - 8px);
          height: calc(100% - 8px);

          border-radius: 26px;
          
          background-color: #fff;

          transition: 250ms linear all;

          &.catalog {
            left: 4px;
            right: 0;
          }

          &.collection {
            right: 4px;
            left: auto;
          }
        }

        &.libary {
          .mobile-switch-selected {
            transform: none;
          }

          .select-libary {
            color: #575B7B;
          }
        }

        &.collection {
          .mobile-switch-selected {
            left: 50%;
          }

          .select-collection {
            color: #575B7B;
          }
        }
      }
    }
  }

  .hidden {
    display: none;
  }
}
</style>
