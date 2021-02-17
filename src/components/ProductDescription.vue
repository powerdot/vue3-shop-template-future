<template>
	<div :class="{full_description:true, show: show}">
		<div class="carousel">
			<flickity ref="flickity" :options="flickityOptions">
				<div class="carousel-cell" v-for="(image, i) of images" :key="`image_${i}`">
					<img :src="image.src" :alt="image.alt">
				</div>
			</flickity>
		</div>

		<div class="about_content">
			<div class="container">
				<div class="row">
					<div class="col-md-6"><div class="product_name">{{name}}
						<div class="status ok" v-if="available">В наличии!</div>
						<div class="status bad" v-else>Нет в наличии</div>
					</div></div>
				</div>
				<div class="row">
					<div class="col-md-7"><div class="product_description">
						<h2>Описание</h2>
						<div class="description" v-html="description"></div>
						<strong v-if='description_alert'><span class="alert_icon"></span><span v-html="description_alert"></span></strong>
						<h2>Комплект</h2>
						<ul class="set">
							<li v-for="(item, i) of set" :key='`set_item_${i}`'>{{item.name}} - {{item.amount}} {{item.measure||"шт"}}.</li>
						</ul>
						<h2>Как использовать?</h2>
						<ul class="how_to_use">
							<li>Подключите USB 3.0 провод в райзер и в PCI-E 1x микросхему;</li>
							<li>Установите райзер на ригу или в любое другое удобное место, зафиксируете его;</li>
							<li>Установите видеокарту на райзер, зафиксируйте её;</li>
							<li>Подключите PCI-E 1x в материнскую плату (подойдут любые PCI-E слоты: 1x и 16x);</li>
						</ul>
						
					</div></div>
					<div class="col-md-5">
						<div class="buy_holder">
							<div class="title">Купить</div>
							<table>
								<tbody>
									<tr>
										<td><button class="buy_amount_changer minus" @click='changeAmount(-1)'></button></td>
										<td><input class="buy_amount" type="text" v-model="amount" placeholder="0" @change="changeAmount"></td>
										<td><button class="buy_amount_changer plus" @click='changeAmount(1)'></button></td>
									</tr>
								</tbody>
							</table>
							<div class="price_per_item" v-if='price_sum != "special"'>Ваша цена: <span>{{price_per_item}}</span> ₽/шт.</div>
							<div class="special" v-else>Пожалуйста, свяжитесь с нами для получения специальных условий при оптовых закупках.</div>
							<div class="summary" v-if='price_sum != "special"'>Итого: <span>{{price_sum}}</span> ₽</div>
							<div class="divider"> <div class="info_icon"></div> </div>
							<div class="prices_rules" v-if='special_price_from'>
								В зависимости от количества товара, вы получите специальную цену!
								<div>от {{special_price_from}}шт - Особые условия</div>
							</div>
							<button class="add_to_cart">Добавить в корзину</button>
						</div>
					</div>
				</div>

				<div class="row">
					<div class="col-md-12"><h2>Посмотрите видео</h2></div>
				</div>
				<div class="row">
					<div class="col-md-4 video" v-for='(video, i) of videos' :key='`video_${i}`'>
						<div class="holder">
							<a target="_blank" :href="`${video.href}`"><div class="image" :style="`background: url(${video.image});`">
								<div class="play_button"></div>
							</div></a>
							<div class="name">{{video.title}}</div>
							<div class="desc">{{video.desc}}</div>
						</div>
					</div>
				</div>
			</div>
		</div>

		<div class="close" @click='close'></div>
	</div>
</template>

<script>
import Flickity from 'vue-flickity';
export default {
	components: {Flickity},
	data() {
		return {
			flickityOptions: {
				contain: false,
				imagesLoaded: true,
				percentPosition: false,
				initialIndex: 1
			},
			show: false,
			name: "Райзер 008C",
			available: true,
			images: [
				{src: "//mircheg.ru/actid.ru/mining/images/risers/1.png", alt: ""},
				{src: "//mircheg.ru/actid.ru/mining/images/risers/2.png", alt: ""},
				{src: "//mircheg.ru/actid.ru/mining/images/risers/4.png", alt: ""}
			],
			amount: 1,
			videos: [
				{
					image: '//i.ytimg.com/vi/Lw9xwd_N4dI/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&amp;rs=AOn4CLDJdBoGhmsd_KzZNSezzRdMmAd7DA',
					title: 'Какие райзеры бывают?',
					desc: 'Узнайте какого типа бывают райзеры и что важно учитывать при их покупке.',
					href: 'https://youtube.com/watch?v=Lw9xwd_N4dI'
				},
				{
					image: '//i.ytimg.com/vi/VJEobSyVaPE/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&amp;rs=AOn4CLCzicQotp_KKbKqXyLxqFho1svJEA',
					title: 'Инструкция по установке',
					desc: 'Криптомайнер с многолетним стажем рассказывает как правильно и в какой последовательности подключать райзеры.',
					href: 'https://youtube.com/watch?v=VJEobSyVaPE'
				},
				{
					image: '//i.ytimg.com/vi/NQZipUriho0/hqdefault.jpg?sqp=-oaymwEZCNACELwBSFXyq4qpAwsIARUAAIhCGAFwAQ==&amp;rs=AOn4CLA4cyUNoargALC6fsTY23RuDxh2pQ',
					title: 'Презентация восьмой версии',
					desc: 'Что изменилось в восьмой версии и почему нужно брать именно её?',
					href: 'https://youtube.com/watch?v=NQZipUriho0'
				},
			],
			description: "Райзеры используются для подключения видеокарт к материнской плате на коротком расстоянии.<br>Райзеры 008S версии обладают тремя портами для подключения питания: MOLEX, PCI-E 6 PIN и SATA, что делает их очень удобными, так как для подключения питания Вам теперь не понадобятся переходники.<br>Восьмая версия является более стабильной и защищенной, чем 006 и 007.",
			description_alert: "Не подключайте одновременно больше одного вида питания к райзеру, иначе он выйдет из строя!",
			set: [
				{name: "PCI-E 1x", amount: 1, measure: "шт"},
				{name: "USB 3.0 60см", amount: 1, measure: "шт"},
				{name: "Райзер 008S", amount: 1, measure: "шт"}
			],
			prices: {
				1: 600,
				5: 550,
				25: 450,
				150: 'special' 
			},
			price_per_item: 0,
			price_sum: 0,
			special_price_from: false
		}
	},
	methods: {
		close(){
			this.show = false;
			document.body.classList.remove('dont_scroll');
		},
		open(data){
			this.show = true;
			document.body.classList.add('dont_scroll');
			this.amount = 1;
			this.images = data.images;
			this.prices = data.prices;
			this.set = data.set;
			this.description = data.description;
			this.description_alert = data.description_alert;
			this.videos = data.videos;
			this.name = data.name;
			this.available = data.available;
			let special_price_entity = Object.entries(this.prices).find(x=>x[1]=='special');
			if(special_price_entity) this.special_price_from = special_price_entity[0];
			this.changeAmount();
			this.$nextTick(() => this.resize())
		},
		resize () {
			this.$refs.flickity.resize()
		},
		getPriceFor(amount){
			var amount_price = 0;
			for(var i=0; i<Object.keys(this.prices).length; i++){
				if( Object.keys(this.prices)[i] > amount ) break;
				amount_price = this.prices[ Object.keys(this.prices)[i] ];
			}
			return amount_price!='special'?amount_price:'special';
		},
		countPriceFor(amount){
			var summ = 0;
			for(var i=1;i<=amount;i++) summ += this.getPriceFor(i) 
			if(typeof summ == "string"){if(summ.indexOf('special')>-1){summ='special';}}
			return summ;
		},
		changeAmount(q){
			let amount = Math.abs(this.amount.toString().replace(/\D+/g, ''));
			if(amount==NaN || amount==undefined || amount==null || amount.toString() == "NaN" || amount==0) amount=1;
			if(typeof q == 'number') amount += q;
			this.amount = amount;
			this.price_sum = this.countPriceFor(amount);
			if(this.price_sum != 'special') this.price_per_item = (this.price_sum/this.amount).toFixed(2);
		}
	},
	mounted () {
		this.$nextTick(() => {
			this.resize()
		});
	}
}
</script>

<style lang="stylus" scoped>
.full_description{
		position: fixed;
		background: white;
		z-index: 3;
		left: 0;
		top: 0;
		height: 100%;
		width: 100%;
		overflow-y: scroll;
		display none;
		&.show{
			display: block;
			.product_name{
				animation-duration: 0.5s;
				animation-name: product_name;
				.status{
					animation-duration: 1s;
					animation-name: product_name_status;
					opacity: 0;
					animation-fill-mode: forwards;
				}
			}
			.product_description{
				animation-duration: 1s;
				animation-name: product_description;
				opacity: 0;
				animation-fill-mode: forwards;
			}
			.buy_holder{
				animation-duration: 1s;
				animation-name: buy_holder;
				animation-fill-mode: forwards;
				opacity: 0;
			}
			.close{
				animation-duration: 1s;
				animation-name: close;
				animation-fill-mode: forwards;
			}
			.carousel{
				animation-duration: 0.5s;
				animation-name: carousel;
			}
		}

		.carousel{
			height: 450px;
			background: white;

			img {
				display: block;
				height: 200px;
			}

			.previous,
			.next{
				display: none;
			}
			.flickity-button{
				display none !important;
			}
		}

		.close{
			background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAEpSURBVGhD7dk9CsJAEIbheABb7fUkHkKPY2krnskz2HoLO0Fn1A+WEEJ2szs/Mi98qKl80E2TLoqi6G9a0I609eeTbnva7vs2P0a8aDeaJuZAe9IetC1fyI2/PCM0MUDwdzjxhdI0MdUQSANTHYEkMc0QSALTHIFaYsQQqAVGHIFqYtQQqAZGHYHmYMwgUAnGHALlYMwi0BSMeQQaw7hBoCGMOwRKMXeaSwRiDCMYwLvQXJb+nXj9M+OiFHGm9c+Mi4YOdnpmXGDG7k5uMFNuseYxUxDILCYHgcxhShDIDGYOAqljaiCQGqYmAoljWiCQGKYlAjXHSCBQM4wkAlXHaCBQNYwmAvUxK1p2/MyOH3dpIRAwV9qSL5S0+b1qx79EMSKKoshaXfcGi/zGyoPvvCcAAAAASUVORK5CYII=");
			background-size: cover;
			background-position: center center;
			background-repeat: no-repeat;
			height: 50px;
			width: 50px;
			position: fixed;
			right: 20px;
			top: 20px;
			cursor: pointer;
			opacity: 0.7;
			&:hover{
				opacity: 1;
			}
		}

		.about_content{
			margin-top: 50px;
			background: linear-gradient(#f5f5f5 0%, #e2e2e2 100%);
			min-height: 500px;
			padding-bottom: 100px;
			padding-top: 50px;
		}

		.product_name{
			font-family: 'Yeseva One';
			font-weight bold;
			font-size: 34pt;
			display: inline-block;
			cursor: default;
			margin-left: 0px;
			transition: 0.7s all;
			position: relative;
			background: white;
			padding: 10px 30px;
			padding-top: 15px;
			box-shadow: 0 0 100px rgba(0,0,0,0.1);
			top: -80px;
			margin-bottom: -70px;
		}

		.alert_icon{
			background: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAALvSURBVGhD7Vg9TxVBFN2IWtjp00rteOyKsSKiVpYm4kcDfv4QzPsBYK0kfrXGAoIJEWwtVGT3ERPh+QP8akSowWLGc8e73d3HzNuZ5Wn2JCdsws6558xcdoaJatSoUR56NhpQK8l5lcUtlcbz+PkZ3MLzb0N6zuIO/65F72od7ePheweVnT6ps/i+SpMfOku0C1WWfDdjVwZPsFx10KtDRzGTTzGjO5I5F5IGwjwiTZYPCxS8A/ObkpkyxCpukDaX8Q/dGT4I48+k4j6JII/16sgBLusHEDwE4ddSwRDESixRTS5fDmbmKzSfEzUXvKxEFW1TRGonttEbsJR3JeEqqbJTN9mOG9THwWOY/V+SqA3fPR/RV8bHDN/jWXrHhlgFfJ2SBtuyBy2fJGjLqxOX9blL1w2v3RgT37ElOmGGbdmBdlgMKrVJeQ6wo5abx9ne7qAtXhJyIbUNhSDzH1703kI50c7TbK876JD195wiC+0VsQpfrQ6A6P0LkkA/ULWbo2yzGFiqljS4L5gm99hmMRDgpTi4D4jumGObxUCAjjTYlfkXKKf0jivxd7DONouBAFvSYFcGCYCNlW0Wo+z3P2eQAPDGNovx7wf4D1poXRrsyiAB0mSNbRYDAealwa4MFMDqM+plIwsUYJJtFsNcOgmDXRkkQDZ0lm0Wgw9z3yQBF/oOgNa2O8wR0EbTkogLAwSYYnu7g6776JsrCdnSZwD0/rbTPzQEc90niNnSb4D4IduyB1I3aOOQBG3oKwB8/FTLw0fYlhtUO7ktiVbKNJ5gO70By/dEFK6AaOMHbKN38NXiglQgJE3N2WiAbZSDudzN4kWpUAii1itvl7s56KIVs1LqssuG9MXRby7u57L+gb68hSAbUvEyJE3Vjse5TFigWAMzNVN2syNCa9vM+tszh1m+OpgdG8cOGPgimetGGgNOOe+wIWAOgO3mKN3bYEbnwDUE26QVMqTnLPnEv5ukU6X1waxGjRpdEEV/ADn2nqaBmKN/AAAAAElFTkSuQmCC");
			background-size: cover;
			background-repeat: no-repeat;
			background-position: center center;
			height: 16px;
			width: 16px;
			margin-right: 5px;
			display: inline-block;
			margin-bottom: -3px;
		}

		strong{
			margin-top: 10px;
			display: inline-block;
		}

		h2{
			margin-top: 30px;
			margin-bottom: 10px;
		}

		ul{
			margin-bottom: 30px;
			font-size: 12pt;
			margin-top: 0px;
		}

		.how_to_use{
			list-style: decimal;
		}
		.buy_holder{
			background: white;
			padding: 15px;
			width: 350px;
			margin: 0 auto;
			box-shadow: 0 0 50px rgba(0,0,0,0.05);
			.title{
				margin: 0 auto;
				display: block;
				width: 90px;
				text-align: center;
				position: relative;
				top: -25px;
				padding: 5px 2px;
				background: white;
				border-radius: 10px;
				color: #a9a9a9;
				text-transform: uppercase;
				font-weight: bold;
				margin-bottom: -10px;
			}
			table{
				margin: 0 auto;
			}
			.summary{
				font-family: 'Yeseva One';
				font-size: 12pt;
				margin-top: 10px;
				text-align: right;
				padding: 5px 10px;
				padding-top: 7px;
			}
		}

		.status{
			background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAFjSURBVEhL7ZK7SgNBGEaXPIAS8IaVnQh5grRiY2EV0oi+gJWvoI0IIY0GtAvYWVgqWkkgiFgExEJFQdRKrEylsuv5x2/FQjYzEsFiDxzm8l8mk9koJ+dHkiQZi+O4Iie13X9ovsNhDubvWFaov9A/vdECGg2F/g4OuTA5vMDYwZtAF9UqGxIbaIxgDY88fdBfX1KrbEisqqCqLS/Ib+Gjlr0h2W5ieL8TuQP4ik1t+UGBeycte0LunP6FeW35QcHXO2krE/I2PtPjUW35QUHQO5F3hR0t/aEofac2561lSU6d0X7UusrDoHDTGvhA7h3DhErDoHCQBrvYxWMssVdMZb2Kz3iLMyoLh+JtNE7QPt0DhSw2y2F2k0t8whccVjgMCs+tkeaH1swFgPmKDprCJc2nFQ6Dwi00TvEN9xX6fiP72tyNWA4pHAaF9kZNvMc9HFfIwXoZr8k7Y/zdbXL+AVH0AZaVM1BCms1cAAAAAElFTkSuQmCC");
			background-size: 18px;
			background-repeat: no-repeat;
			background-position: 3px 3px;
			border-radius: 4px;
			color: white;
			width: 7px;
			height: 25px;
			cursor: default;
			font-size: 10pt;
			font-family: sans-serif;
			overflow: hidden;
			position: absolute;
			left: calc(100% - 15px);
			bottom: 5px;
			padding-left: 26px;
			padding-top: 3px;
			transition: 0.2s all;
			&.bad{
				background-color: #f44336;
			}
			&.ok{
				background-color: #4CAF50;
			}
			&:hover{
				width: 105px;
			}
		}
			

		.carousel {
			background: white;
		}

		.full_description .carousel img {
			display: block;
			height: 200px;
		}

		.carousel .previous,
		.carousel .next{
			display: none;
		}

	}

@media screen and ( min-width: 768px ) {
	.full_description .carousel img {
		height: 400px;
	}
}




@keyframes carousel {
	0%   {opacity: 0; top: -100px;}
	100% {opacity: 1; top: 0px;}
}

@keyframes product_name {
	0%   {opacity: 0; top: 0px;}
	100% {opacity: 1; top: -80px;}
}

@keyframes product_name_status{
	50% {opacity: 0; }
	100% {opacity: 1; }
}


@keyframes product_description{
	0%   {opacity: 0; top: 100px; position: relative;}
	100% {opacity: 1; top: 0px; position: relative;}
}


@keyframes buy_holder{
	0%   {opacity: 0; top: 100px; position: relative;}
	100% {opacity: 1; top: 0px; position: relative;}
}

@keyframes close{
	0%   {transform: rotate(0) scale(0);}
	50%   {transform: rotate(0) scale(0);}
	75% {transform: rotate(0) scale(1.5);}
	100% {transform: rotate(0deg) scale(1);}
}



input.buy_amount{
	outline: none;
	border: none;
	text-align: center;
	width: 50px;
	font-size: 16pt;
	font-weight: bold;
}
.buy_amount_changer{
	height: 23px;
	width: 50px;
	background-position: center center !important;
	background-repeat: no-repeat !important;
	background-size: 16px !important;
	cursor: pointer;
	opacity: 0.4;
	border: none;
	outline: none;
	background: white;
	&:hover{
		opacity: 1;
	}
	&:active{
		transform: scale(1.1);
	}
	&.plus{
		background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAABiSURBVEhLYxjxgAeIz0AxiE0zwA/E/6EYxKYZGLWIbDBqEdmAKhbxAbEgASwPxDCLQGxsapAxyEwMcAmIYYZQC4PMxAB0s4huQUcMGFqpjhgwahHZYNQisgHdGieDHTAwAADbg1cRWwqYnwAAAABJRU5ErkJggg==");
	}
	&.minus{
		background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAA0SURBVEhLYxgFo2AUjILBAfiAWJDKGGQmBrgExP+pjEFmYgC6WUS3oBsFo2AUjAK6AgYGABoFLgFUNFwJAAAAAElFTkSuQmCC");
	}
}


.special{
	text-align: center;
	font-size: 10pt;
	padding: 30px 0;
}

.divider{
	margin: 0 auto;
	width: 260px;
	opacity: 0.4;
}
.divider:before, .divider:after{
	display: inline-block;
	width: 100px;
	height: 1px;
	background: gray;
	content: "-";
	font-size: 0;
	position: relative;
	top: -11px;
}
.divider .info_icon{
	display: inline-block;
	height: 23px;
	width: 50px;
	background-position: center center !important;
	background-repeat: no-repeat !important;
	background-size: 16px !important;
	background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAGNSURBVEhL5ZU3TsRAFEAXaEk14RrkDoGgIlwBCkJJKJEI4hAchDuQhMQVAJGOABK8Z42bXc94dleigCc9yTP2fNt/vr8b/5Y+nMVdPAnu4Az2YtcM4xm+43fENzzFIeyIJfxAg13hPk7gaNBj567Ra3yYRWyLTfzCJ1x1ooY1fEbXbDiRwzK64BZHnMjEa+/QtbVvZp5N1yOannYZQ7NgGgediHGO5nulGFVzGYyxjsawQCqxTK2gm2IU5yKYwrS/YmXpz6FPsleMuuMAjeV31sI2enKyGMU5CqaYQmNtFaMm/No96YameAimGEdjGbOFX7tRbupybpRMnU3Tk3XFkHOjQzTWdDFqoixvSzNF3Y160BgvGO3sdmqfJNXfcj/Yyv0psW2ULaiuKKpwjc3VzAw4kcKGaGO0QbbTVO2N9+jaeSdysNW7wKfzF5DCPSl/E5+Y/Zso8c3KH5+bayVZtqZHrSjnfHOvMV0L2BHumV3YBmmwKj3nNf3YNZapDdIP8DjosW8YLeG/TKPxA/OXb2Yspy4HAAAAAElFTkSuQmCC");
}

.prices_rules{
	text-align: center;
	color: gray;
	cursor: default;
}
.prices_rules div{
	margin-top: 5px;
	font-size: 10pt;
}

.add_to_cart{
	margin: 0 auto;
	border: 1px solid #4caf50;
	padding: 10px 30px;
	display: block;
	margin-top: 30px;
	color: #1c8820;
	border-radius: 4px;
	cursor: pointer;
}
.add_to_cart:hover{
	background: #4caf50;
	color: white;
}

.price_per_item{
	text-align: center;
	margin-top: 10px;
	font-size: 9pt;
	color: gray;
}


.video{
	.image{
		background-size: cover !important;
		background-repeat: no-repeat !important;
		background-position: center center !important;
		width: 100%;
		height: 210px;
		border-radius: 4px;
		overflow: hidden;
	}
	.play_button{
		background-color: rgba(0,0,0,0);
		background-image: url("data:image/png;base64,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");
		height: 100%;
		width: 100%;
		background-size: 0px;
		background-position: center center;
		background-repeat: no-repeat;
		transition: 0.2s;
		background-color: rgba(0,0,0,0.2);
		background-size: 50px;
		cursor: pointer;
		&:hover{
			background-color: rgba(0,0,0,0.3);
			background-size: 64px;
		}
	}
	.name{
		padding: 5px 0px;
		font-size: 13pt;
		font-weight: bold;
		color: blue;
		cursor: pointer;
	}
	.desc{
		font-size: 12pt;
		color: gray;
		cursor: default;
	}
}


</style>