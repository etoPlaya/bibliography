<template>
  <div class="modal-background" role="dialog" aria-modal="true" tabindex="-1">
    <form class="modal" @submit.prevent="onSubmit">
      <a href="" class="close" @click.prevent="closeModal">
        <CloseIcon />
      </a>

      <div class="modal-title">Добавление своей книги</div>

      <div class="modal-fields">
        <div class="modal-group">
          <div class="modal-group-subtitle">Тип источника</div>
          <div class="modal-group-radios">
            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="type" 
                id="type-1" 
                value="Книга"
              />
              <label for="type-1">
                <i class="circle"></i>
                <div class="name">Книга</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="type" 
                id="type-2" 
                value="Статья из журнала"
              />
              <label for="type-2">
                <i class="circle"></i>
                <div class="name">Статья из журнала</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="type" 
                id="type-3" 
                value="Статья из газеты"
              />
              <label for="type-3">
                <i class="circle"></i>
                <div class="name">Статья из газеты</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                  type="radio" 
                  v-model="type" 
                  id="type-4" 
                  value="Статья из сборника"
                />
              <label for="type-4">
                <i class="circle"></i>
                <div class="name">Статья из сборника</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                  type="radio" 
                  v-model="type" 
                  id="type-5" 
                  value="Диссертация"
                />
              <label for="type-5">
                <i class="circle"></i>
                <div class="name">Диссертация</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                  type="radio"
                  v-model="type" 
                  id="type-6" 
                  value="Автореферат"
                />
              <label for="type-6">
                <i class="circle"></i>
                <div class="name">Автореферат</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="type" 
                id="type-7" 
                value="Закон, акт и т.п."
              />
              <label for="type-7">
                <i class="circle"></i>
                <div class="name">Закон, акт и т.п.</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="type" 
                id="type-8" 
                value="Интернет-ресурс"
              />
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
              <input 
                type="radio" 
                v-model="quantity" 
                id="quantity-1" 
                value="1-3 автора"
              />
              <label for="quantity-1">
                <i class="circle"></i>
                <div class="name">1-3 автора</div>
              </label>
            </div>

            <div class="modal-group-radio">
              <input 
                type="radio" 
                v-model="quantity" 
                id="quantity-2" 
                value="Более 3-х авторов и/или под редакцией"
              />
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
              <input 
                type="text" 
                placeholder="Иванов А.К., Джеймс К" 
                v-model="bookAuthors"
              />
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

  mounted() {
    window.onkeydown = function( event ) {
    if ( event.keyCode == 27 ) {
        taxi.$emit('hiddenModal');
      }
    };
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
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
@import '@/styles/button.scss';

@import '@/styles/modal.scss';
</style>