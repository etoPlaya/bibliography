<template>
  <div class="result">
    <div class="result-head">
      <div class="result-total">
        <span>{{ books.length }}</span> 
        результатов
      </div>

      <a href="" class="result-clear" @click.prevent="$emit('clearResult')">
        <span>очистить</span>
        <CloseIcon/>
      </a>
    </div>

    <div class="result-list">
      <div class="result-item" v-for="book of books">
        <a href="" class="result-item-link">
          <LinkIcon/>
        </a>

        <div class="result-item-title">
          {{ book.title + ',' }}
          {{ book.year + 'г.'}}
          {{ book.isbn }}
        </div>

        <a href="" class="result-item-button" @click.prevent="addBookInCollection(book)">
          <AddIcon/>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { taxi } from "../main";

import LinkIcon from '@/assets/ui/link.svg';
import AddIcon from '@/assets/ui/add.svg';
import CloseIcon from '@/assets/ui/close.svg';

export default {
  components: {
    LinkIcon,
    AddIcon,
    CloseIcon,
  },
  
  data() {
    return {
      books: [
        {
          title: 'Богатый Папа, Бедный Папа',
          publisher: 'Роберт Кийосаки',
          year: 1994,
          isbn: '978-985-15-3255-7',
          type: 'Финансы домашнего хозяйства'
        },
        {
          title: 'Самый богатый человек в Вавилоне',
          publisher: 'Джордж Самюэль Клейсон',
          year: 1926,
          isbn: '978-985-15-4829-9',
          type: 'Управление частным капиталом'
        },
        {
          title: 'Alibaba. История мирового восхождения от первого лица',
          publisher: 'Дункан Кларк',
          year: 2019,
          type: 'Биография'
        },
        {
          title: 'Одна привычка в неделю: Измени себя за год',
          publisher: 'Бретт Блюменталь',
          year: 2015,
          type: 'Литература по саморазвитию'
        },
        {
          title: 'Почему вы глупы, больны и бедны... И как стать умным, здоровым и богатым!',
          publisher: 'Рэнди Пол Гейдж',
          year: 2006,
          type: 'Литература по саморазвитию'
        },
        {
          title: 'Как завоевывать друзей и оказывать влияние на людей',
          publisher: 'Дейл Карнеги',
          year: 1936,
          isbn: '5-289-01225-7',
          type: 'Литература по саморазвитию'
        },
      ]
    }
  },

  methods: {
    addBookInCollection(book) {
      taxi.$emit('visibleCollection');
      taxi.$emit('addBookInCollection', book);
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

.result {
  margin-top: 30px;

  &-head {
  display: flex;
  align-items: center;
  }

  &-total {
  font-size: 18px;
  line-height: 23px;
  color: $brand;

  margin-right: 10px;
  }

  &-clear {
    display: flex;
    align-items: center;
    border-radius: 4px;
    cursor: pointer;

    padding: 4px 5px;

    transition: 250ms ease all;

    &:hover {
      background: #F3F3F7;
    }

    &:active, &.active {
      background: #D4D4E2;
    }

    span {
      font-size: 12px;
      color: #82859E;
    }

    svg {
      fill: #82859E;
      margin-left: 3.5px;
    }
  }

  &-list {
    margin: 12px -24px 0 0;
    overflow-y: auto;

    max-height: calc(100vh - 328px);

    padding: 0 24px 20px 0;

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
  }

  &-item {
    display: flex;
    align-items: center;
    padding: 11px 5px 11px 5px;
    border-bottom: 1px solid $background;

    transition: 250ms ease all;

    &:hover {
      background-color: #F9F9FB;
    }

    &:first-child {
      border-top: 1px solid $background;
    }

    &-link {
      display: block;
      margin-right: 9px;

      padding: 5px;
      border-radius: 4px;
      transition: 250ms ease all;

      &:hover {
        background: #F2F2F5;

        svg {
          stroke: #A9ABBC;
        }
      }

      &:active, &.active {
        background: #D7D7E0;

        svg {
          stroke: #70728F;
        }
      }

      svg {
        fill: transparent;
        stroke: #BEBFCC;
        stroke-width: 2px;
        transition: 250ms ease all;
      }
    }

    &-title {
      font-size: 15px;
      color: $brand;
    }

    &-button {
      display: block;
      margin-left: auto;

      padding: 5px;
      border-radius: 4px;

      transition: 250ms ease all;

      &:hover {
        background-color: #F2F2F5;

        svg {
          fill: #A9ABBC;
        }
      }

      &:active, &.active {
        background: #D7D7E0;

        svg {
          fill: #70728F;
        }
      }

      svg {
        fill: #BEBFCC;
        transition: 250ms ease all;
      }
    }
  }	
}
</style>