<template>
	<section>
		<div class="tabs">
			<div class="tabs-tab">
				<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
					<circle cx="7.5" cy="7.5" r="5.5" stroke-width="2"/>
					<path d="M12 12L14 14"  stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
				<span>Поиск</span>
			</div>
			<div class="tabs-tab">
				<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
					<path d="M11.775 7.83586L13.2522 6.35868C14.2493 5.36157 14.2493 3.74493 13.2522 2.74782C12.2551 1.75071 10.6384 1.75071 9.6413 2.74782L7.74456 4.64458C5.218 7.18755 10.4802 9.14444 8.06799 11.5429L6.3587 13.2522C5.36159 14.2493 3.74495 14.2493 2.74784 13.2522C1.75072 12.255 1.75072 10.6384 2.74784 9.64129L3.89675 8.49238" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
				</svg>
				<span>Полезные ссылки</span>
			</div>
		</div>
		<div class="search">
			<p class="search-desc">Чтобы найти получить библиографическое описание, найдите источник литературы по названию, автору или ISBN</p>
			<form>
				<div class="wrapper">
					<input type="text" placeholder="Прозведение, автор, название, ISBN">
					<button class="button">Найти</button>
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Год издания">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Издательство">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Категория">
				</div>
				<div class="wrapper">
					<input type="text" placeholder="Язык">
				</div>
			</form>
		</div>
	</section>
</template>

<script>
export default {
 data() {
 }
}
</script>

<style lang="scss" scoped>
@import '@/styles/mixin.scss';
@import '@/styles/variable.scss';
	section {
		max-width: 950px;
		width: 100%;

		height: calc(100% - 69px);
		height: calc(100vh - 69px);

		padding: 20px 40px;
		background: #FFFFFF;
		box-shadow: 0px 4px 64px rgba(0, 0, 0, 0.33);
		border-radius: 0px 40px 0px 0px;
		@media screen and (max-width: 768px) {
			height: auto;
		}
		.tabs {
			display: flex;
			align-items: center;
			&-tab {
				display: flex;
				align-items: center;

				margin-right: 25px;

				cursor: pointer;
				transition: 250ms ease all;
				&:hover:not(.active) {
					opacity: .7;
				}
				&.active {
					span, svg {
						color: $brand;
						stroke: $brand;
					}
				}
				svg {
					display: block;

					fill: transparent;
					stroke: #A5A8C0;

					margin-right: 4px;
				}
				span {
					font-size: 16px;
					line-height: 20px;
					color: #A5A8C0;
				}
			}
		}
		.search {
			margin-top: 24px;
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
					}
				}
			}
		}
	}
</style>