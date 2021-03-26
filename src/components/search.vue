<template>
	<div class="search-container">
		<div class="search">
			<p class="search-desc">Чтобы найти получить библиографическое описание, найдите источник литературы по названию, автору или ISBN</p>
			<form @submit.prevent="onSubmit">
				<div class="wrapper">
					<input type="text" placeholder="Прозведение, автор, название, ISBN" v-model="bookTitle">
					<button class="button">Найти</button>
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Год издания" v-model="bookYear">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Издательство" v-model="bookDevelop">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Категория" v-model="bookCategory">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Язык" v-model="bookLanguage">
				</div>
			</form>
		</div>
		<div class="result" v-if="visibleResult">
			<div class="result-head">
				<div class="result-total"><span>{{ books.length }}</span> результатов</div>
				<div class="result-clear" tabindex="1" @click="clearResult">
					<span>очистить</span>
					<svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
						<path fill-rule="evenodd" clip-rule="evenodd" d="M8 2.5C4.96243 2.5 2.5 4.96243 2.5 8C2.5 11.0376 4.96243 13.5 8 13.5C11.0376 13.5 13.5 11.0376 13.5 8C13.5 4.96243 11.0376 2.5 8 2.5ZM1.5 8C1.5 4.41015 4.41015 1.5 8 1.5C11.5899 1.5 14.5 4.41015 14.5 8C14.5 11.5899 11.5899 14.5 8 14.5C4.41015 14.5 1.5 11.5899 1.5 8ZM5.64645 5.64645C5.84171 5.45118 6.15829 5.45118 6.35355 5.64645L8 7.29289L9.64645 5.64645C9.84171 5.45118 10.1583 5.45118 10.3536 5.64645C10.5488 5.84171 10.5488 6.15829 10.3536 6.35355L8.70711 8L10.3536 9.64645C10.5488 9.84171 10.5488 10.1583 10.3536 10.3536C10.1583 10.5488 9.84171 10.5488 9.64645 10.3536L8 8.70711L6.35355 10.3536C6.15829 10.5488 5.84171 10.5488 5.64645 10.3536C5.45118 10.1583 5.45118 9.84171 5.64645 9.64645L7.29289 8L5.64645 6.35355C5.45118 6.15829 5.45118 5.84171 5.64645 5.64645Z"/>
					</svg>
				</div>
			</div>
			<div class="result-list">
				<div class="result-item" v-for="book of books">
					<a href="" class="result-item-link">
						<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
							<path d="M11.775 7.83586L13.2522 6.35868C14.2493 5.36157 14.2493 3.74493 13.2522 2.74782C12.2551 1.75071 10.6384 1.75071 9.6413 2.74782L7.74456 4.64458C5.218 7.18755 10.4802 9.14444 8.06799 11.5429L6.3587 13.2522C5.36159 14.2493 3.74495 14.2493 2.74784 13.2522C1.75072 12.255 1.75072 10.6384 2.74784 9.64129L3.89675 8.49238" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
						</svg>
					</a>
					<div class="result-item-title">
            {{ isString(book.title) }}
            {{ isString(book.year) }}
            {{ book.isbn != '' ? book.isbn : ''}}
          </div>
					<a href="" class="result-item-button">
						<svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
							<path fill-rule="evenodd" clip-rule="evenodd" d="M7 2C4.23858 2 2 4.23858 2 7C2 9.76142 4.23858 12 7 12C9.76142 12 12 9.76142 12 7C12 4.23858 9.76142 2 7 2ZM0 7C0 3.13401 3.13401 0 7 0C10.866 0 14 3.13401 14 7C14 10.866 10.866 14 7 14C3.13401 14 0 10.866 0 7ZM7 4C7.55228 4 8 4.44772 8 5V6H9C9.55228 6 10 6.44771 10 7C10 7.55228 9.55229 8 9 8H8V9C8 9.55229 7.55228 10 7 10C6.44772 10 6 9.55229 6 9V8H5C4.44772 8 4 7.55228 4 7C4 6.44772 4.44771 6 5 6H6V5C6 4.44772 6.44772 4 7 4Z"/>
						</svg>
					</a>
				</div>
			</div>
		</div>
		<div class="no-books" v-if="!visibleResult">
			<img src="@/assets/books.png" alt="">
			<p>В нашей базе содержится <br> более 2 000 000 источников информации</p>
		</div>
	</div>
</template>

<script>
export default {
 	data() {
	 	return {
			visibleResult: false,
			bookTitle: '',
			bookYear: '',
			bookDevelop: '',
			bookCategory: '',
			bookLanguage: '',
      books: [
        {
          title: 'Богатый Папа, Бедный Папа',
          publisher: 'Роберт Кийосаки',
          year: '1994 г',
          isbn: '978-985-15-3255-7',
          type: 'Финансы домашнего хозяйства'
        },
        {
          title: 'Самый богатый человек в Вавилоне',
          publisher: 'Джордж Самюэль Клейсон',
          year: '1926 г',
          isbn: '978-985-15-4829-9',
          type: 'Управление частным капиталом'
        },
        {
          title: 'Alibaba. История мирового восхождения от первого лица',
          publisher: 'Дункан Кларк',
          year: '2019 г',
          type: 'Биография'
        },
        {
          title: 'Одна привычка в неделю: Измени себя за год',
          publisher: 'Бретт Блюменталь',
          year: '2015 г',
          type: 'Литература по саморазвитию'
        },
        {
          title: 'Почему вы глупы, больны и бедны... И как стать умным, здоровым и богатым!',
          publisher: 'Рэнди Пол Гейдж',
          year: '2006 г',
          type: 'Литература по саморазвитию'
        },
        {
          title: 'Как завоевывать друзей и оказывать влияние на людей',
          publisher: 'Дейл Карнеги',
          year: '1936 г',
          isbn: '5-289-01225-7',
          type: 'Литература по саморазвитию'
        }
      ]
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
			

			this.visibleResult = false
		},
    isString(string) {
      if(string != '' && string != undefined) {
        return string + '.'
      } else {
        return '';
      }
    }
	}
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
.search-container {
	margin-top: 24px;
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
					@include placeholder {
						color: #BEBFCC;
						transition: 250ms ease all;
					}
					&:hover,&:focus {
						@include placeholder {
							color: $brand;
						}
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
						background-color: $brandHover;
					}
				}
			}
		}
	}
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
			cursor: pointer;
			outline: none;

			transition: 250ms ease all;
			&:hover,&:focus {
				opacity: .7;
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

      padding-right: 24px;

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
			padding: 16px 5px;
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
				&:hover svg {
					stroke: $brand;
				}
				svg {
					fill: transparent;
					stroke: #BEBFCC;
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
				&:hover svg {
					fill: $brand;
				}
				svg {
					fill: #BEBFCC;
					transition: 250ms ease all;
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