<template>
  <div class="collection-dist">
    <div class="title">Сформировав свой список литературы, вы можете скачать его или распечатать. Также вам всегда будет доступна эта сборка по ссылке.</div>
    <div class="wrapper">
      <div class="link">
        <span>http://bigraph.ru/c/Jgeo_F7FG</span>
        <a href="">
          <CopyIcon/>
        </a>
      </div>

      <a href="" class="button">Распечатать</a>

      <a href="" class="button">Скачать pdf</a>
    </div>
  </div>
</template>

<script>
import CopyIcon from '@/assets/ui/copy.svg';

export default {
  components: {
    CopyIcon,
  }
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

.collection-dist {
  background: #787B96;
  border-radius: 8px;

  padding: 20px;
  margin-top: 15px;

  .title {
    max-width: 540px;

    font-size: 14px;
    line-height: 18px;
    color: #FFFFFF;

    @include mobile {
      font-size: 12px;
      line-height: 15px;
    }
  }

  .wrapper {
    display: flex;
    align-items: center;

    margin-top: 18px;

    .link {
      display: flex;
      justify-content: space-between;
      align-items: center;

      max-width: 405px;
      width: 100%;
      height: 44px;

      background: #F3F3F7;
      border-radius: 8px;

      padding: 0 12px;
      margin-right: 40px;

      @include mobile {
        margin-right: 0;
      }
      
      span {
        font-size: 14px;
        line-height: 18px;
        color: #595D7E;
      }
      
      a {
        border-radius: 4px;
        
        padding: 5px;

        transition: 250ms ease all;

        &:hover {
          background: #E1E2EA;
        }
      }

      svg {
        display: block;
        width: 12px;
        height: 14px;
        
        fill: #BEBFCC;
        stroke-width: 2px;
      }
    }

    .button {
      display: flex;
      justify-content: center;
      align-items: center;

      max-width: 196px;
      width: 100%;
      height: 44px;

      background: #F3F3F7;
      border-radius: 8px;

      font-size: 14px;
      font-weight: bold;
      line-height: 18px;
      color: #595D7E;

      transition: 250ms ease all;

      @include mobile {
        display: none;
      }

      &:not(:last-child) {
        margin-right: 13px;
      }

      &:hover {
        background: #D7D7E0;
      }

      &.active, &:active {
        background: #AEAEC1;
      }
    }
  }
}
</style>