<template>
	<view>
		<text>123</text>
	</view>
</template>
<!--async  1,2,3,4,5 -->
<!--  1,3,2,4,5 -->


<script>
	export default {
		data() {
			return {
				pageQuery: false
			}
		},
		onLoad(option) {
			console.log('onLoad => ' + JSON.stringify(option))
			this.pageQuery = option
		},
		_mounted() {
			console.log('mounted mock fetch data =》' + JSON.stringify(this.pageQuery))
			let res = this.getLocation().then(r => {
				res = this.getWeather().then(r => {
					res = this.getGoods().then(r => console.log(r))
					res = Promise.all([this.getOtherA(), this.getOtherB()]).then(r => console.log(r))
				}).catch(oo => console.error(oo))
			}).catch(oo => console.error(oo))

		},
		async mounted() {
			console.log('mounted mock fetch data =》' + JSON.stringify(this.pageQuery))
			uni.showLoading({
				title: 'get Data ing '
			})
			try {
				let res = await this.getLocation()
				console.log(res)
				res = await this.getWeather()
				console.log(res)
				res = await this.getGoods()
				console.log(res)
				res = await Promise.all([this.getOtherA(), this.getOtherB()])
				console.log(res)
			} catch(e) {
				uni.hideLoading()
				uni.showToast({
					icon: 'none',
					title: 'get fail => ' + e
				})
			}
		},
		methods: {
			getLocation() {
				return new Promise((resolve,reject) => {
					setTimeout(() => resolve('location get it!'), 2000)
				})
			},
			getWeather() {
				return new Promise((resolve,reject) => {
					setTimeout(() => reject('weather get it!'), 2000)
				})
			},
			getGoods() {
				return new Promise(resolve => {
					setTimeout(() => resolve('goods get it!'), 2000)
				})
			},
			getOtherA() {
				return new Promise(resolve => {
					setTimeout(() => resolve('otherA get it!'), 2000)
				})
			},
			getOtherB() {
				return new Promise(resolve => {
					setTimeout(() => resolve('otherB get it!'), 2000)
				})
			},
		}
	}
</script>

<style>

</style>
