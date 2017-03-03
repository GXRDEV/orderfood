<template>
	<div class="food" v-if="showFood">
		
	</div>
	
</template>

<script>
	export default{
		props:{
			selectedFood:{
				type:Object
			}
			
		},
		data(){
			return{
				showFood:false
			}
		},
		methods:{
			
		}
	}
</script>

<style lang="scss" scoped>
	.food{
		position: fixed;
		width: 100%;
		height:100%;
		top: 0;
		background: #fff;
	}
</style>