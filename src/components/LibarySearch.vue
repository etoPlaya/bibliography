<template>
  <div class="search-container">
    <div class="search">
      <p class="search-desc">Чтобы найти получить библиографическое описание, найдите источник литературы по названию, автору или ISBN</p>
      <form @submit.prevent="onSubmit">
        <div class="wrapper">
          <input 
            type="text" 
            v-model="bookTitle"
            :placeholder="searchPlaceholder"
          >

          <button class="button dark-btn">Найти</button>
        </div>

        <div class="row">
            <input 
              type="text" 
              placeholder="Год издания" 
              v-model="bookYear"
            >

            <input 
              type="text" 
              placeholder="Издательство" 
              v-model="bookDevelop"
            >

            <input 
              type="text" 
              placeholder="Категория" 
              v-model="bookCategory"
            >

            <input 
              type="text" 
              placeholder="Язык" 
              v-model="bookLanguage"
            >
        </div>
      </form>
    </div>

    <LibarySearchResult 
      v-if="visibleResult" 
      @clearResult="clearResult"
    />

    <div class="no-books" v-if="!visibleResult">
      <img src="@/assets/books.png" alt="">
      <p>В нашей базе содержится <br> более 2 000 000 источников информации</p>
    </div>
  </div>
</template>

<script>
import LibarySearchResult from '@/components/LibarySearchResult';

export default {
  components: {
    LibarySearchResult
  },

  data() {
    return {
      visibleResult: false,
      bookTitle: '',
      bookYear: '',
      bookDevelop: '',
      bookCategory: '',
      bookLanguage: '',
      searchPlaceholder: '',
      templatePlaceholder: 'Прозведение, автор, название, ISBN',
    }
  },

  mounted() {
    this.editPlaceholder();

    window.addEventListener('resize', this.editPlaceholder, { passive: true });
  },

  methods: {
    onSubmit(evt) {
      let inputsValue = [this.bookTitle, this.bookYear, this.bookDevelop, this.bookCategory, this.bookLanguage];

      inputsValue.forEach(element => {
        element != '' ? this.visibleResult = true : false;
      });
    },

    clearResult(evt) {
      this.bookTitle = '';
      this.bookYear = '';
      this.bookDevelop = '';
      this.bookCategory = '';
      this.bookLanguage = '';


      this.visibleResult = false;
    },

    editPlaceholder() {
      if(window.innerWidth < 500) {
        this.searchPlaceholder = 
        this.templatePlaceholder.split('').splice(0, 18).join('') + '...';
      } else {
        this.searchPlaceholder = this.templatePlaceholder;
      }
    }
  },
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
@import '@/styles/button.scss';

.search-container {
  margin-top: 24px - 6px;

  .search {
    &-desc {
      max-width: 340px;
      font-size: 12px;
      line-height: 15px;

      color: $brand;

      @include mobile {
        display: none;
      }
    }

    form {
      display: flex;
      flex-wrap: wrap;
      width: 100%;

      margin: 12px 0 0 0;

      input {
        position: relative;

        max-width: 120px;
        width: 100%;
        height: 32px;

        border-radius: 6px;

        font-size: 13px;
        color: $brand;

        background-color: $background;
        

        padding-left: 8px;
        transition: 250ms ease all;
        
        @include placeholder {
          color: #BEBFCC;
          transition: 250ms ease all;
        }

        &:hover {
          background: #E7E8EE;
        }
      }

      .wrapper {
        position: relative;
        margin: 0 16px 15px 0;

        max-width: 870px;
        width: 100%;
        margin: 0 0 12px 0;

        @include mobile {
          margin-bottom: 8px;
        }

        input {
          max-width: none;
          height: 44px;

          font-size: 14px;

          padding-left: 16px;
        }

        .button {
          position: absolute;
          top: 4px;
          right: 4px;

          width: 80px;
          height: 36px;

          font-size: 14px;
          line-height: 18px;

          cursor: pointer;

          @include mobile {
            width: 74px;
            height: 36px;
          }
        }
      }

      .row {
        display: flex;
        flex-wrap: wrap;
        width: 100%;

        @include mobile {
          justify-content: space-between;
        }
        
        input {
          margin: 0 16px 8px 0;

          &:last-child {
            margin-right: 0;
          }

          @include mobile {
            max-width: calc(50% - 10px);
            margin-right: 0;
          }
        }
      }
    }
  }

  .no-books {
    position: absolute;
    top: calc(50% - 100px);
    width: calc(100% - 80px);

    @media screen and (max-height: 700px) {
      top: 50%;
    }

    @include mobile {
      position: static;
      margin: 80px auto 0 auto;
    }

    img {
      display: block;
      max-width: 100%;

      margin: 0 auto;

      @include mobile {
        max-width: 136px;
      }
    }

    p {
      font-size: 18px;
      line-height: 23px;
      text-align: center;
      color: #C6C7D2;

      margin-top: 30px;

      @include mobile {
        font-size: 13px;
        line-height: 16px;

        margin-top: 8px;
      }
    }
  }
}
</style>