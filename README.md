一、转场效果。
(1)方法一:在路由文件中设置meta为数字,meta表示其路由的深度,然后在App.vue中设置(监听$route,根绝to、from meta值得大小设置不同的跳转动画。)

<template>
	<div id="app">
		<transition :name="transitionName">
			<navigation>
				<router-view class="child-view"></router-view>
			</navigation>
		</transition>
	</div>
</template>

<script>
	export default {
		name: 'App',
		data () {
			return {
				transitionName: ''
			}
		},
        watch: {
			'$route' (to, from) {
				let mb = typeof(to.meta) == 'number' ? to.meta : 1;       // 目标
				let fyd = typeof(from.meta) == 'number' ? from.meta : 1;  // 源
				this.transitionName = mb > fyd ? 'slide-right' : 'slide-left'
			}
		}
	}
</script>

(2)方法二:通过插件vue-navigation来实现(更加方便,无须对router进行多余的设置)。npm i -S vue-navigation安装,在main.js导入
import Navigation from 'vue-navigation'
Vue.use(Navigation, {router}) // router为路由文件
在App.vue中设置:
this.$navigation.on('forward', (to, from) => {
    this.transitionName = 'fade-right'
 })
 this.$navigation.on('back', (to, from) => {
    this.transitionName = 'fade-left'
 })
 this.$navigation.on('replace', (to, from) => {
    this.transitionName = 'fade'
 })
附上代码文件
