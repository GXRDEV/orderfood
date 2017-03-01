<template>
	<div class="shopcart">
		<div class="shop-left">
			<div class="icon" :class="{'heightlight':shoucount>0}">购</div>
			<span class="count" v-show="shoucount>0">{{shoucount}}</span>
			<span class="money"><b :class="{'heighttext':totalPrice>0}">￥{{totalPrice}}</b></span>
			<span class="deliveryPrice">另需配送费{{deliveryPrice}}元</span>
		</div>
		<div class="shop-right" :class="addClass">
			{{send}}
		</div>
	</div>
</template>

<script>
	export default{
		props:{
			deliveryPrice:{
				type:Number
			},
			minPrice:{
				type:Number
			},
			selectFoods:{
				type:Array,
				default(){
					return [
						{
							price:10,
							count:2
						}
					]
				}
			}
		},
		computed:{
			totalPrice(){
				let total=0;
				this.selectFoods.forEach((food)=>{
					total+=food.price*food.count
				})
				return total
			},
			shoucount(){
				let count = 0;
				this.selectFoods.forEach((food)=>{
					count += food.count
				})
				return count
			},
			send(){
				if(this.totalPrice=0){
					return `￥${this.minPrice}元起送 `
				}else if(this.totalPrice<this.minPrice){
					let money=this.minPrice-this.totalPrice
					return `还差￥${money}元起送 `	
				}else{
					return `去结算`
				}
				
			},
			addClass(){
				if(this.totalPrice<this.minPrice){
					return ""
				}else{
					return "lightbj"
				}
			}
			
		}
	}
</script>


<style lang="scss">
	.shopcart{
		height: .96rem;
		background:#131d26;
		.shop-left{
			float:left;
			.icon{
				position: absolute;
				height: .88rem;
				width: .88rem;
				background:#2b343d;
				bottom: 0;
				left: .15rem;
				border: .16rem solid #131d26;
				border-radius: 50%;
				font-size: .5rem;
				color: #fff;
				text-align: center;
				line-height: .88rem;
			}
			.heightlight{
				background: rgb(0,160,220);
			}
			.count{
				position: absolute;
				left: 1rem;
				bottom: .8rem;
				font-size: .24rem;
				border-radius: .5rem;
				height: .3rem;
				width: .48rem;
				text-align: center;
				line-height: .35rem;
				color: #fff;
				background: #FF0000;
			}
			.heighttext{
				color: #fff;
			}
			.money{
				float: left;
				margin-left: 1.4rem;
				font-size: .32rem;
				line-height: .96rem;
				color: #9b9b9d;
				b{
					font-weight: bold;
					padding-right: .12rem;
					border-right:1px solid #9B9FA2;
				}
			}
			.deliveryPrice{
				padding-left: .12rem;
				float: left;
				font-size:.24rem;
				line-height: .96rem;
				color: #9B9FA2;
			}
		}
		.shop-right{
			height: 100%;
			width: 2.1rem;
			background: #2b343b;
			float: right;
			font-size: .24rem;
			color: #9b9fa2;
			font-weight: bold;
			text-align: center;
			line-height: .96rem;
		}
		.lightbj{
			background: #00b43c;
			color: #fff;
		}
	}
</style>