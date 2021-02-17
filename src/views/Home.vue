<template>
	<div class='welcome'>
		<div class='partner'></div>
		<div class='by_center'>
			<h1>Будущее уже здесь</h1>
			<button>Купить</button>
		</div>
		<img src="../assets/gif.gif" class="ball">
	</div>
	<div class="container loveyou">
		<div class="row">
			<div class="col text">
				Твоя ферма - это ферма №1 для нас<br>
				<span>По-этому, мы <b>проверяем</b> каждое устройство, которое закупаем и только <b>потом продаем</b>.</span>
			</div>
		</div>
	</div>
	<div class="container">
		<Item @openProductPage="productClick" :item="item" v-for='(item,i) of items' :key='`item_${i}`'/>
	</div>
	<div style='height: 300px;'></div>
	<ProductDescription ref="pd"/>
</template>

<script>
import Item from '../components/Item';
import ProductDescription from '../components/ProductDescription';

export default {
	name: 'Main',
	components: {
		Item,
		ProductDescription
	},
	data(){
		return {
			items: [
				{
					name: "Райзер 001S",
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
					description: "Райзеры 001S используются для подключения видеокарт к материнской плате на коротком расстоянии.<br>Райзеры 008S версии обладают тремя портами для подключения питания: MOLEX, PCI-E 6 PIN и SATA, что делает их очень удобными, так как для подключения питания Вам теперь не понадобятся переходники.<br>Восьмая версия является более стабильной и защищенной, чем 006 и 007.",
					description_alert: "Не подключайте одновременно больше одного вида питания к райзеру, иначе он выйдет из строя!",
					set: [
						{name: "PCI-E 1x", amount: 1, measure: "шт"}
					],
					prices: {
						1: 300,
						5: 250,
						25: 200,
						100: 'special' 
					},
				},
				{
					name: "Райзер 002S",
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
					description: "Райзеры 002S используются для подключения видеокарт к материнской плате на коротком расстоянии.<br>Райзеры 008S версии обладают тремя портами для подключения питания: MOLEX, PCI-E 6 PIN и SATA, что делает их очень удобными, так как для подключения питания Вам теперь не понадобятся переходники.<br>Восьмая версия является более стабильной и защищенной, чем 006 и 007.",
					description_alert: "Не подключайте одновременно больше одного вида питания к райзеру, иначе он выйдет из строя!",
					set: [
						{name: "PCI-E 1x", amount: 1, measure: "шт"},
						{name: "USB 3.0 60см", amount: 1, measure: "шт"}
					],
					prices: {
						1: 400,
						5: 350,
						25: 300,
						125: 'special' 
					},
				},
				{
					name: "Райзер 003S",
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
					description: "Райзеры 003S используются для подключения видеокарт к материнской плате на коротком расстоянии.<br>Райзеры 008S версии обладают тремя портами для подключения питания: MOLEX, PCI-E 6 PIN и SATA, что делает их очень удобными, так как для подключения питания Вам теперь не понадобятся переходники.<br>Восьмая версия является более стабильной и защищенной, чем 006 и 007.",
					description_alert: "Не подключайте одновременно больше одного вида питания к райзеру, иначе он выйдет из строя!",
					set: [
						{name: "PCI-E 1x", amount: 1, measure: "шт"},
						{name: "USB 3.0 60см", amount: 1, measure: "шт"},
						{name: "Райзер 008S", amount: 1, measure: "шт"}
					],
					prices: {
						1: 500,
						5: 450,
						25: 400,
						150: 'special' 
					},
				}
			]
		};
	},
	methods: {
		productClick(data){
			this.$refs.pd.open(data);
		}
	}
}
</script>

<style lang="stylus" scoped>

.welcome{
		background: #003d7a;
		background: linear-gradient(135deg, #0068d0 0%,#022731 100%);
		height 100vh;
	
		h1{
			color: white;
			text-transform: uppercase;
			font-family: 'Commissioner';
			font-weight bold;
		}

		button{
			border: 1px solid white;
			padding: 12px 40px;
			border-radius: 5px;
			background: rgba(0,0,0,0);
			color: white;
			cursor: pointer;
			font-size: 11pt;
			display: block;
			margin: 0 auto;
			margin-top: 70px;

			&:hover{
				background: rgba(255,255,255,0.1);
			}
		}


		.ball{
			position: absolute;
			left: 50%;
			bottom: -250px;
			width: 500px;
			margin-left: -250px;
		}

	 .partner{
			width: 80px;
			height: 100px;
			position: absolute;
			left: 100px;
			background: white;
			background-image: url(../assets/actm.png);
			background-repeat:no-repeat;
			background-size: 90%;
			background-position: center center;
			box-shadow: 0 0 50px rgba(0,0,0,0.1);
	}
}


.loveyou{
	margin-bottom 40px;
	.text{
		width: 900px;
		margin-top: 200px;
		font-size: 21pt;
		font-family: 'Yeseva One';
		font-weight: 900;
		span{
			font-size: 16pt;
			margin-top: 10px;
			background: #022731;
			color: white;
			padding: 2px;
		}
	}
}






	.screen{
		position: relative;
		width: 1200px;
		margin: 0 auto;
		margin-bottom: 100px;
	}
	.fullscreen{
		height: 100vh;
		width: 100%;
	}
	.by_center{
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%);
	}
	.hidden{
		display: none;
	}
</style>