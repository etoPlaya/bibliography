<template>
  <section>
    <div class="collection" v-if="visibleCollection">
      <div class="collection-head">
        <div class="title">Моя литература</div>

        <a href="" class="clear">
          <span>очистить</span>
          <CloseIcon/>
        </a>

        <a href="" class="added">
          <span>добавить свой источник</span>
          <AddIcon/>
        </a>
      </div>

      <CollectionDist/>

      <CollectionList/>
    </div>

    <div class="no-collection" v-if="!visibleCollection">
      <div class="title">Моя литература</div>

      <div class="placeholder">
        Выбери книги из поиска слева, чтобы скачать их описание списком или 
        <a href="" @click.prevent="visibleCollection = !visibleCollection">добавь свою книгу</a>
      </div>

      <img src="@/assets/collection.png" alt="">
    </div>
  </section>
</template>

<script>
import CloseIcon from '@/assets/ui/close.svg';
import AddIcon from '@/assets/ui/add.svg';

import CollectionDist from '@/components/CollectionDist';
import CollectionList from '@/components/CollectionList';

export default {
  components: {
    CloseIcon,
    AddIcon,
    CollectionDist,
    CollectionList,
  },
  data() {
    return {
      visibleCollection: false,
    }
  }
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

  @media screen and (max-width: 768px) {
    height: auto;
  }

  .collection {
    &-head {
      display: flex;
      align-items: center;

      .title {
        font-size: 18px;
        line-height: 23px;
        color: #FFFFFF;

        margin-right: 11px;
      }

      .clear {
        display: flex;
        align-items: center;

        font-size: 12px;
        color: #82859E;

        padding: 5px;
        border-radius: 4px;

        transition: 250ms ease all;
        
        &:hover {
          background: rgba(243, 243, 247, 0.1);
          color: #B2B4C3;

          svg {
            fill: #B2B4C3;
          }
        }

        &:active, &.active {
          background: rgba(255, 255, 255, 0.5);
          color: #EEEFF2;

          svg {
            fill: #EEEFF2;
          }
        }

        svg {
          display: block;

          fill: #82859E;

          margin-left: 4px;
        }
      }

      .added {
        display: flex;
        align-items: center;

        font-size: 12px;
        color: #82859E;

        padding: 5px;
        border-radius: 4px;

        margin-left: auto;

        transition: 250ms ease all;

        &:hover {
          background: rgba(243, 243, 247, 0.1);
          color: #B2B4C3;

          svg {
            fill: #B2B4C3;
          }
        }

        &:active, &.active {
          background: rgba(255, 255, 255, 0.5);
          color: #EEEFF2;

          svg {
            fill: #EEEFF2;
          }
        }

        svg {
          display: block;

          fill: #82859E;
          
          margin-left: 4px;
        }
      }
    }
  }

  .no-collection {
    position: absolute;
    top: calc(50% - 200px);
    width: calc(100% - 80px);

    .title {
      font-size: 18px;
      line-height: 23px;
      color: #FFFFFF;
      text-align: center;
    }

    .placeholder {
      max-width: 388px;

      font-size: 18px;
      line-height: 23px;
      color: #C6C7D2;
      text-align: center;
      
      background: #787B96;
      border-radius: 8px;

      padding: 22px 44px;
      margin: 20px auto 0 auto;

      a {
        color: inherit;
        text-decoration: underline;

        &:hover {
          text-decoration: none;
        }
      }
    }

    img {
      display: block;
      margin: 32px auto 0 auto;
    }
  }
}
</style>