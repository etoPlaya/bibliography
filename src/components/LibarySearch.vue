<template>
	<div class="search-container">
		<div class="search">
			<p class="search-desc">Чтобы найти получить библиографическое описание, найдите источник литературы по названию, автору или ISBN</p>

			<form @submit.prevent="onSubmit">
				<div class="wrapper">

					<input 
            type="text" 
            placeholder="Прозведение, автор, название, ISBN" 
            v-model="bookTitle"
          >

					<button class="button">Найти</button>
				</div>

				<div class="wrapper">
					<input 
            type="text" 
            placeholder="Год издания" 
            v-model="bookYear"
          >
				</div>

				<div class="wrapper">
					<input 
            type="text" 
            placeholder="Издательство" 
            v-model="bookDevelop"
          >
				</div>

				<div class="wrapper">
					<input 
            type="text" 
            placeholder="Категория" 
            v-model="bookCategory"
          >
				</div>

				<div class="wrapper">
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
			<img 
        src="@/assets/books.png" 
        alt=""
      >
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
	 	}
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
		}
	}
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';

.search-container {
	margin-top: 24px - 6px;
	.search {
		&-desc {
			max-width: 340px;
			font-size: 12px;
			line-height: 15px;

			color: $brand;
		}
		form {
			display: flex;
			flex-wrap: wrap;
			width: 100%;

			margin: 12px 0 0 0;
			.wrapper {
				position: relative;
				margin: 0 16px 0 0;

				&:first-child {
					max-width: 870px;
					width: 100%;
					margin: 0 0 12px 0;
					input {
						max-width: none;
						height: 44px;

						font-size: 14px;

						padding-left: 16px;
					}
				}

				input {
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

				.button {
					position: absolute;
					top: 4px;
					right: 4px;

					width: 80px;
					height: 36px;

					font-size: 14px;
					line-height: 18px;
					color: #FFFFFF;

					border-radius: 4px;
					background-color: $brand;

					cursor: pointer;
					transition: 250ms ease all;
					&:hover {
						background: #464863;
					}
          &:active, &.active {
            background: #2A2C3C;
          }
				}
			}
		}
	}
	.no-books {
		position: absolute;
		top: calc(50% - 100px);
		width: calc(100% - 80px);
		img {
			display: block;
			max-width: 100%;

			margin: 0 auto;
		}
		p {
			font-size: 18px;
			line-height: 23px;
			text-align: center;
			color: #C6C7D2;

			margin-top: 30px;
		}
	}
}
</style>