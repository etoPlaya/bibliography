<template>
  <section>
  <div class="tabs">
    <div class="tabs-tab" @click="visibleSearch = true" :class="{ active: visibleSearch }">
      <svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
        <circle cx="7.5" cy="7.5" r="5.5" stroke-width="2"/>
        <path d="M12 12L14 14"  stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      <span>Поиск</span>
    </div>

    <div class="tabs-tab" @click="visibleSearch = false" :class="{ active: !visibleSearch }">
      <svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
        <path d="M11.775 7.83586L13.2522 6.35868C14.2493 5.36157 14.2493 3.74493 13.2522 2.74782C12.2551 1.75071 10.6384 1.75071 9.6413 2.74782L7.74456 4.64458C5.218 7.18755 10.4802 9.14444 8.06799 11.5429L6.3587 13.2522C5.36159 14.2493 3.74495 14.2493 2.74784 13.2522C1.75072 12.255 1.75072 10.6384 2.74784 9.64129L3.89675 8.49238" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
      <span>Полезные ссылки</span>
    </div>

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

export default {
  components: {
    LibarySearch,
    LibaryLinks,
  },
  data: () => ({
    visibleSearch: true
  })
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

section {
  position: relative;

  max-width: 950px;
  width: 100%;

  height: calc(100% - 69px);
  height: calc(100vh - 69px);

  padding: 20px 40px;
  background: #FFFFFF;
  box-shadow: 0px 4px 64px rgba(0, 0, 0, 0.33);
  border-radius: 0px 40px 0px 0px;

  overflow: hidden;

  @media screen and (max-width: 768px) {
  height: auto;
  }

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

      &:hover:not(.active) {
        background-color: $background;

        svg {
          stroke: $brand;
        }

        span {
          color: $brand;
        }
      }

      &.active {
        span, svg {
          color: $brand;
          stroke: $brand;
        }
      }

      svg {
        display: block;

        fill: transparent;
        stroke: #A5A8C0;

        margin-right: 4px;

        transition: 250ms ease all;
      }

      span {
        font-size: 16px;
        line-height: 20px;
        color: #A5A8C0;
      }
    }
  }
}
</style>