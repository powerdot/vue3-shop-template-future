<template>
	<div :class='{row:true, item:true, image_hover: productImageHover}'>
		<div class='col-md-2'>
			<div class='image_holder'>
				<img ref="productImage" class='product_image' src="../assets/goods/IMG_9111.png" alt="" @mouseover="mouseOver" @mouseleave="mouseLeave">
			</div>
		</div>
		<div class='col-md-8'>
			<div class='name' @click="openProductPage">{{item.name}}</div>
			<div class='description' v-html="item.description"></div>
		</div>
		<div class='col-md-2'>
			<div class='price_holder'>
				<div class='price'>от <span>{{lowest_price}} ₽</span></div> 
				<button class='buy_button' @click="openProductPage">Купить</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Item',
	props: {
		item: {
			type: Object,
			default: ()=>{}
		}
	},
	data(){
		return {
			productId: -1,
			productImageHover: false,
			lowest_price: 0
		}
	},
	methods: {
		mouseOver(){
			this.productImageHover = true;
		},
		mouseLeave(){
			this.productImageHover = false;
		},
		openProductPage(){
			this.$emit("openProductPage", this.item)
		},
		findLowestPrice(){
			let values = Object.entries(this.item.prices).filter(x=>typeof x[1]=='number').map(x=>x[1]);
			this.lowest_price = Math.min(...values);
		}
	},
	mounted(){
		this.findLowestPrice();
	}
}
</script>

<style lang="stylus" scoped>
.item{
	margin-top: 50px;

	&:hover{
		.name{
			background: #ffffaf;
		}
	}

	.product_image{
		height: 100%;
		width: 100%;
		background-position: center center !important;
		background-size: 100%;
		background-repeat: no-repeat;
		transition: 1s all;
		object-fit: contain;
	}
	
	.image_holder{
		width: 200px;
		height: 250px;
		margin: 0 auto;
		transform: scale(1);
		left: 0;
		transition: 0.5s all;
		z-index: 2;
		position: relative;
		background: url(../assets/boom.gif);
		background-size: 0%;
		background-repeat: no-repeat;
		background-position: center center;
		&:hover{
			background-size: 100%;
			transform: scale(1.75);
			left: 100px;
			.product_image{
				background-size: 70%;
			}
		}
	}
	
	
	.name{
		font-family: 'Yeseva One';
		font-size: 26pt;
		display: inline-block;
		cursor: default;
		margin-left: 0px;
		transition: 0.7s all;
	}
	
	.description{
		cursor: default;
		position: relative;
		z-index: 2;
		left: 10px;
		transition: 0.6s all;
		background: white;
		box-shadow: 0 0 0 none;
		transform: scale(1);
		padding: 10px 20px;
	}

	&.image_hover{
		.description{
			transform: scale(1.1) translateY(10px);
			box-shadow: 0 0 50px rgba(0,0,0,0.1);
			left: 80px;
			.buy_button{
				visibility unset;
			}
		}
		.name{
			padding-left: 160px;
		}
	} 
	
	.price_holder{
		width: 122px;
		display: block;
		margin: 0 auto;

		.price{
			font-size: 16pt;
			font-family: 'Commissioner';
			cursor: default;
			font-weight bold;
			span{
				background: #00f;
				color: #fff;
				padding: 14px;
				padding-bottom: 5px;
				padding-top: 3px;
			}
		}
		
		.buy_button{
			border: 1px solid blue;
			color: blue;
			width: 122px;
			margin-top: 10px;
			padding: 10px 0px;
			cursor: pointer;
			outline: none;
			&:hover{
				color: white;
				background: blue;
			}
		}
	}
	
	
	.prices{
		color: gray;
		text-align: center;
		margin-top: 20px;
		font-size: 8pt;
		cursor: default;
		div{
			margin-top: 5px;
		}
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
}
</style>