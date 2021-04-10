<template>
  <div class="links-container">
    <p>Советуем ознакомиться с библиографией как с наукой и посмотреть, чему каждый может научиться</p>
    <div class="blocks">
      <a :href="'https://' + link.site" class="block" v-for="link of links" target="_blank">
        <div class="title">
          {{ link.title.length >= 55 ? link.title.slice(0, 55) + '...' : link.title }}
        </div>
        <div class="wrapper">
          <div class="search">Читать</div>
          <div class="page">{{link.site}}</div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    links: [
      {title: 'Как составлять библиографи-ческое описание, чтобы не об', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
      {title: 'Что такое библиография?', site: 'wikipedia.org'},
      {title: 'Как составлять библиографи-ческое описание, чтобы не обосраться', site: 'rsl.ru'},
    ]
  }),
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

.links-container {
  margin-top: 24px;

  p {
    max-width: 390px;
    font-size: 12px;
    line-height: 15px;
    color: #585C7D;
  }

  .blocks {
    display: flex;
    flex-wrap: wrap;
    margin: 16px -25px -20px 0;
    padding-top: 10px;

    overflow-y: auto;

    max-height: calc(100vh - 169px);
    
    padding-bottom: 20px;
    &::-webkit-scrollbar {
      width: 6px;
    }

    /* Track */
    &::-webkit-scrollbar-track {
      background: #F3F3F7;
      border-radius: 2px;
    }

    /* Handle */
    &::-webkit-scrollbar-thumb {
      background: #C2C2D6;
      border-radius: 2px;
    }

    /* Handle on hover */
    &::-webkit-scrollbar-thumb:hover {
      background: #AEAEC1;
    }

    .block {
      display: flex;
      flex-direction: column;

      max-width: calc(33% - 25px);
      width: 100%;
      min-height: 100px;
      background: linear-gradient(73.28deg, #595D7E 0%, #595D7E 0.01%, #7B80A2 100%);

      border-radius: 8px;

      padding: 15px 12px 16px 16px;
      margin: 0 25px 20px 0;
      cursor: pointer;

      transition: 250ms ease all;

      &:hover {
        box-shadow: 0px 12px 30px rgba(89, 93, 126, 0.6);
        transform: translateY(-5px);

        .title {
          color: #FFFFFF;
        }

        .wrapper {
          .search {
            color: #CFD1DD;

            &:after {
              color: #CFD1DD;
            }
          }
        }
      }

      .title {
        font-size: 16px;
        line-height: 20px;

        color: #CFD1DD;

        padding-bottom: 8px;

        transition: 250ms ease all;
      }

      .wrapper {
        display: flex;
        justify-content: space-between;
        align-items: center;

        margin-top: auto;

        .search {
          font-size: 16px;
          line-height: 20px;

          color: #A5A8C0;

          &:after {
            content: '\2794';
            font-size: 14px;
            line-height: 20px;
            padding-left: 3px;

            color: #A5A8C0;

            vertical-align: middle;

            transition: 250ms ease all;
          }
        }

        .page {
          font-size: 12px;
          line-height: 15px;
          color: #A5A8C0;
        }
      }
    }
  }
}
</style>