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
//		watch: {
//			'$route' (to, from) {
//				let mb = typeof(to.meta) == 'number' ? to.meta : 1;       // 目标
//				let fyd = typeof(from.meta) == 'number' ? from.meta : 1;  // 源
//				this.transitionName = mb > fyd ? 'slide-right' : 'slide-left'
//			}
//		},
		created () {
			this.$navigation.on('forward', (to, from) => {
		    this.transitionName = 'slide-right'
		 })
		 this.$navigation.on('back', (to, from) => {
		    this.transitionName = 'slide-left'
		 })
		 this.$navigation.on('replace', (to, from) => {
		    this.transitionName = 'slide'
		 })
		}
	}
</script>

<style>
	html, body, div {
		height: 100%;
	}

	body {
		margin: 0;
	}

	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
	}

	.child-view {
  		position: absolute;
  		width: 100%;
  		transition: all .5s cubic-bezier(.55,0,.1,1);
	}

	.slide-left-enter, .slide-right-leave-active {
  		opacity: 0;
  		-webkit-transform: translate(30px, 0);
  		transform: translate(30px, 0);
	}
	
	.slide-left-leave-active, .slide-right-enter {
  		opacity: 0;
  		-webkit-transform: translate(-30px, 0);
  		transform: translate(-30px, 0);
	}
</style>
