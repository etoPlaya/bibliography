<template>
  <section>
  <div class="tabs">
    <a 
      href="" 
      class="tabs-tab" 
      @click.prevent="visibleSearch = true" 
      :class="{ active: visibleSearch }"
    >
      <LoopIcon />
      <span>Поиск</span>
    </a>

    <a 
      href="" 
      class="tabs-tab" 
      @click.prevent="visibleSearch = false" 
      :class="{ active: !visibleSearch }"
    >
      <LinkIcon/>
      <span>Полезные ссылки</span>
    </a>

  </div>

  <div class="tab-item">
    <LibarySearch v-if="visibleSearch"/>

    <LibaryLinks v-if="!visibleSearch"/>
  </div>
  </section>
</template>

<script>
import LibarySearch from '@/components/LibarySearch';
import LibaryLinks from '@/components/LibaryLinks';

import LoopIcon from '@/assets/ui/loop.svg';
import LinkIcon from '@/assets/ui/link.svg';

export default {
  components: {
    LibarySearch,
    LibaryLinks,
    LoopIcon,
    LinkIcon,
  },
  
  data() {
    return {
      visibleSearch: true,
    }
  },
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

section {
  position: relative;

  max-width: 950px;
  width: 100%;

  height: 100%;

  padding: 20px 40px;
  background: #FFFFFF;
  box-shadow: 0px 4px 64px rgba(0, 0, 0, 0.33);
  border-radius: 0px 40px 0px 0px;

  overflow: hidden;

  .tabs {
    display: flex;
    align-items: center;

    &-tab {
      display: flex;
      align-items: center;

      margin-right: 25px;
      padding: 6px 5px;

      cursor: pointer;
      transition: 250ms ease all;
      border-radius: 5px;

      svg {
        display: block;

        fill: transparent;
        stroke: #A5A8C0;
        stroke-width: 2px;

        margin-right: 4px;

        transition: 250ms ease all;
      }

      span {
        font-size: 16px;
        line-height: 20px;
        color: #A5A8C0;
      }

      &.active {
        span, svg {
          color: $brand;
          stroke: $brand;
        }
      }

      &:hover:not(.active) {
        background-color: $background;

        svg {
          stroke: $brand;
        }

        span {
          color: $brand;
        }
      }
    }
  }

  @include mobile {
    border-radius: 20px 20px 0 0;
    padding: 20px;

    min-height: 100%;
    height: auto;
    overflow: visible;
  }
}
</style>