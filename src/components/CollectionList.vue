<template>
  <div class="collection-list">
    <div class="collection-item" v-for="(book, index) of collectionBooks" v-bind:key="index">
      <a href="" class="collection-item-link">
        <LinkIcon/>
      </a>

      <div class="collection-item-title">
        {{ book.title + ',' }}
        {{ book.year != undefined ? `${book.year} г.` : ''}}
        {{ book.isbn }}
        {{ book.publisher }}
      </div>

      <a href="" class="collection-item-button collection-item-button__edit" 
        @click.prevent="editCurrentBook(book, index)">
        <EditIcon/>
      </a>

      <a href="" class="collection-item-button collection-item-button__copy">
        <CopyIcon/>
      </a>

      <a href="" class="collection-item-button collection-item-button__close" @click.prevent="removeBook(index)">
        <CloseIcon/>
      </a>
    </div>
  </div>
</template>

<script>
import { taxi } from "../main";

import LinkIcon from '@/assets/ui/link.svg';
import EditIcon from '@/assets/ui/edit.svg';
import CopyIcon from '@/assets/ui/copy.svg';
import CloseIcon from '@/assets/ui/close.svg';

export default {
  components: {
    LinkIcon,
    EditIcon,
    CopyIcon,
    CloseIcon,
  },

  data() {
    return {
      collectionBooks: [],
    }
  },

  methods: {
    removeBook(index) {
      this.collectionBooks.splice(index, 1);

      this.collectionBooks.length <= 0 ? taxi.$emit('hiddenCollection') : false; 
    },

    editCurrentBook(book, index) {
      taxi.$emit('visibleModalEdit');

      setTimeout(function() {
        taxi.$emit('editBook', book, index);
      }, 0)
    },
  },

  created() {
    taxi.$on('addBookInCollection', data => {
      this.collectionBooks.push({title: data.title, year: data.year, isbn: data.isbn});
    });
    
    taxi.$on('clearCollection', () => {
      this.collectionBooks = [];
    });

    taxi.$on('replaceBook', (book, index) => {
      this.collectionBooks[index] = book;
    });
  },
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

.collection-list {
  margin: 24px -24px 0 0;
  overflow-y: auto;

  max-height: calc(100vh - 308px);

  padding: 0 24px 20px 0;

  @include mobile {
    max-height: none;
    overflow: visible;

    margin: 40px 0 0 0;
    padding: 0 0 64px 0;
  }

  &::-webkit-scrollbar {
    width: 6px;

    @include mobile {
      display: none;
    }
  }

  /* Track */
  &::-webkit-scrollbar-track {
    background: #696C8A;
    border-radius: 2px;
  }

  /* Handle */
  &::-webkit-scrollbar-thumb {
    background: #9697B0;
    border-radius: 2px;
  }

  /* Handle on hover */
  &::-webkit-scrollbar-thumb:hover {
    background: #AEAEC1;
  }
}

.collection-item {
  display: flex;
  align-items: center;
  padding: 11px 5px 11px 5px;
  border-bottom: 1px solid #787B96;

  transition: 250ms ease all;

  &:hover {
    background-color: #515573;
  }

  &:first-child {
    border-top: 1px solid #787B96;
  }

  &-link {
    display: block;
    margin-right: 9px;

    padding: 5px;
    border-radius: 4px;
    transition: 250ms ease all;

    @include mobile {
      display: none;
    }

    &:hover {
      background: #666A87;

      svg {
        stroke: #9D9FB4;
      }
    }

    &:active, &.active {
      background: #7F839E;

      svg {
        stroke: #D7D7E0;
      }
    }

    svg {
      fill: transparent;
      stroke: #6D708E;;
      stroke-width: 2px;
      transition: 250ms ease all;
    }
  }

  &-title {
    font-size: 15px;
    color: #DEDFE5;
  }

  &-button {
    display: block;

    padding: 5px;
    margin-right: 3px;

    border-radius: 4px;

    transition: 250ms ease all;

    &:last-child {
      margin-right: 0;
    }

    &:hover {
      background-color: #F2F2F5;
    }

    &:active, &.active {
      background: #D7D7E0;
    }

    &__edit {
      margin-left: auto;
      
      svg {
        fill: transparent;
      }
    }

    &__copy {
      svg {
        fill: #6D708E;
      }
    }

    &__close {
      svg {
        fill: transparent;
        stroke: #6D708E;
      }
    }

    svg {
      display: block;
      width: 16px;
      height: 16px;

      transition: 250ms ease all;
    }
  }
}	
</style>