<template>
	<view class="bg-gray-9 h-screen pt-1">
		<view class="text-center mx-10 mt-10  text-xl  bg-blue-3 h-60 rounded-xs flex-center ">
			手撸一套低成本的原子类css
		</view>
		<view class="demo__wrapper mx-10  text-sm">
			<view class="bg-green-6 mt-6 p-10 rounded-xs leading-24" v-for="item in content_list" :key="item">
				{{item}}
			</view>
		</view>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				content_list: [
					'写法简单，都是用sass最基本的语法生成',
					'如使用@while，生成.w-{val},循环批量生成多个样式',
					'如使用@if、@else，在变量$color_num == 0的时候生成bg-blue,其它条件生成bg-blue-{val}',
					'如@each，循环便利颜色数组便利$color_list，批量生成样式',
					'如index()，获取索引值',
					'如nth()，根据索引值，获取数组便利的值',
				]
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss">
	body,
	html {
		margin: 0;
		padding: 0;
	}
</style>
