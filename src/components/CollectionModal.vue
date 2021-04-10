<template>
  <div class="background" role="dialog" aria-modal="true" tabindex="-1">
    <form class="modal" @submit.prevent="onSubmit">
      <a href="" class="close" @click.prevent="closeModal">
        <CloseIcon/>
      </a>

      <div class="modal-title">Добавление своей книги</div>

      <div class="modal-fields">
        <div class="modal-group">
          <div class="modal-group-subtitle">Тип источника</div>
          <div class="modal-group-radios">

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-1" value="Книга">
              <label for="type-1">
                <i class="circle"></i>
                <div class="name">Книга</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-2" value="Статья из журнала">
              <label for="type-2">
                <i class="circle"></i>
                <div class="name">Статья из журнала</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-3" value="Статья из газеты">
              <label for="type-3">
                <i class="circle"></i>
                <div class="name">Статья из газеты</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-4" value="Статья из сборника">
              <label for="type-4">
                <i class="circle"></i>
                <div class="name">Статья из сборника</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-5" value="Диссертация">
              <label for="type-5">
                <i class="circle"></i>
                <div class="name">Диссертация</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-6" value="Автореферат">
              <label for="type-6">
                <i class="circle"></i>
                <div class="name">Автореферат</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-7" value="Закон, акт и т.п.">
              <label for="type-7">
                <i class="circle"></i>
                <div class="name">Закон, акт и т.п.</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="type" id="type-8" value="Интернет-ресурс">
              <label for="type-8">
                <i class="circle"></i>
                <div class="name">Интернет-ресурс</div>
              </label>
            </div>
          </div>

        </div>

        <div class="modal-group">
          <div class="modal-group-subtitle">Количество источников</div>
          <div class="modal-group-radios">

            <div class="modal-group-radio">
              <input type="radio" v-model="quantity" id="quantity-1" value="1-3 автора">
              <label for="quantity-1">
                <i class="circle"></i>
                <div class="name">1-3 автора</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input type="radio" v-model="quantity" id="quantity-2" value="Более 3-х авторов и/или под редакцией">
              <label for="quantity-2">
                <i class="circle"></i>
                <div class="name">Более 3-х авторов и/или под редакцией</div>
              </label>
            </div>

          </div>
        </div>

        <div class="modal-group">

          <div class="modal-group-inputs">
            <label class="modal-group-input">
              <div class="label">ФИО авторов через запятую</div>
              <input type="text" placeholder="Иванов А.К., Джеймс К" v-model="bookAuthors">
              <div class="error">Поле не может быть пустым</div>
            </label>
          </div>

        </div>
      </div>

      <div class="modal-footer">
        <a href="" class="modal-footer-back light-btn" @click.prevent="closeModal">Отменить</a>
        <button class="modal-footer-submit dark-btn">Добавить источник</button>
      </div>
    </form>
    <a href="" class="hidden-closure-area" @click.prevent="closeModal"></a>
  </div>
</template>

<script>
import { taxi } from "../main";

import CloseIcon from '@/assets/ui/close.svg';

export default {
  components: {
    CloseIcon,
  },
  data() {
    return {
      type: '',
      quantity: '',
      bookAuthors: '',
    }
  },
  methods: {
    onSubmit() {
      if(this.bookAuthors != '') {
        taxi.$emit('hiddenModal');
        taxi.$emit('visibleCollection');
        taxi.$emit('addBookInCollection', {title: this.bookAuthors});
      } else {
        const inputs = document.querySelectorAll('.modal-group-inputs input');
        
        inputs.forEach(i => {
          i.value == '' ? i.classList.add('has-error') : false 
        });
      }
    },
    closeModal() {
      taxi.$emit('hiddenModal');
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
@import '@/styles/button.scss';

.background {
  position: fixed;
  top: 0; right: 0; bottom: 0; left: 0;
  width: 100%;
  height: 100%;
  background: rgba(89, 93, 126, 0.75);
}

.hidden-closure-area {
  position: fixed;
  top: 0; right: 0; bottom: 0; left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;

  z-index: 1;
}

.modal {
  position: absolute;

  max-width: 680px;
  width: 100%;
  background: #FFFFFF;
  box-shadow: 0px 4px 64px rgba(0, 0, 0, 0.33);
  border-radius: 8px;

  padding-top: 20px;

  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  z-index: 2;

  &-fields {
    margin-top: 15px;
    padding: 0 20px;
  }

  .close {
    position: absolute;
    top: -17px;
    right: -17px;

    &:hover {
      svg {
        opacity: .3;
      }
    }

    svg {
      display: block;
      width: 14px;
      height: 14px;
      fill: #fff;

      transition: 250ms ease all;
    }
  }

  &-title {
    font-size: 18px;
    line-height: 23px;
    color: #595D7E;

    padding: 0 20px;
  }

  &-group {
    margin-bottom: 20px;

    &-subtitle {
      font-size: 14px;
      line-height: 18px;
      color: #595D7E;
    }

    &-radios {
      display: flex;
      flex-wrap: wrap;
      
      margin: 8px -12px -8px 0;
    }

    &-radio {
      margin: 0 12px 8px 0;

      input[type="radio"] {
        display: none;

        &:checked ~ label {
          .circle {
            background: #999DB7;

            &:before {
              background: #575B7B;
              opacity: 1;
            }
          }

          &:hover {
            background: #F3F3F7;

            .circle {
              background: #8286A6;

              &:before {
                background: #575B7B;
                opacity: 1;
              }
            }
          }

          &:active {
            background: #E1E2EA;

            .circle {
              background: #6A6F95;

              &:before {
                background: #575B7B;
                opacity: 1;
              }
            }
          }
          
          &:focus {
            border-color: #C3C5D5;
            border-width: 2px;
          }
        }
      }

      label {
        display: flex;
        align-items: center;
        justify-content: space-between;

        border: 1px solid #EDEEF2;
        border-radius: 4px;

        padding: 12px;
        cursor: pointer;

        transition: 250ms ease all;

        &:hover {
          background: #F3F3F7;
          border-color: #E1E2EA;

          .circle {
            background: #E1E2EA;

            &:before {
              background: #9B9EB8;
              opacity: 1;
            }
          }
        }

        &:active {
          background: #E1E2EA;
          border-color: #EDEEF2;

          .circle {
            background: #C3C5D5;

            &:before {
              background: #74789C;
              opacity: 1;
            }
          }
        }
        
        &:focus {
          border-color: #C3C5D5;
          border-width: 2px;
        }

        .circle {
          display: flex;
          justify-content: center;
          align-items: center;

          width: 16px;
          height: 16px;

          background: #EDEEF2;
          border-radius: 50%;

          margin-right: 15px;

          transition: 250ms ease all;

          &:before {
            content: '';
            display: block;

            width: 8px;
            height: 8px;

            background: #9B9EB8;
            border-radius: 8px;

            transition: 250ms ease all;

            opacity: 0;
          }
        }

        .name {
          font-size: 13px;
          color: #575B7B;
        }
      }
    }

    &-inputs {
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    }

    &-input {
      position: relative;
      max-width: calc(50% - 10px);
      width: 100%;

      .label {
        font-size: 14px;
        color: #595D7E;
      }

      input {
        display: block;
        width: 100%;
        height: 32px;

        background: #F3F3F7;
        border-radius: 6px;

        font-size: 13px;
        color: #575B7B;

        padding: 0 8px;
        margin-top: 8px;

        border: 2px solid transparent;

        transition: 250ms ease all;

        &:hover {
          background: #E7E8EE;
        }

        @include placeholder {
          font-size: 13px;
          color: #BEBFCC;
        }

        &.has-error {
          border: 2px solid rgba(255, 102, 102, 0.25);

          & ~ .error {
            opacity: 1;
          }
        }
      }

      .error {
        display: block;

        position: absolute;
        bottom: -15px;
        left: 8px;

        font-size: 11px;
        line-height: 13px;
        color: #FF6666;

        transition: 250ms ease all;

        opacity: 0;
      }
    }
  }

  &-footer {
    display: flex;
    align-items: center;
    justify-content: flex-end;

    background: #FFFFFF;
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.16);

    padding: 22px;

    border-radius: 0px 0px 8px 8px;

    &-back {
      display: flex;
      align-items: center;
      justify-content: center;

      width: 99px;
      height: 36px;

      font-size: 14px;

      margin-right: 16px;
    }

    &-submit {
      display: flex;
      align-items: center;
      justify-content: center;
      
      width: 160px;
      height: 36px;

      font-size: 14px;

      cursor: pointer;
    }
  }
}
</style>