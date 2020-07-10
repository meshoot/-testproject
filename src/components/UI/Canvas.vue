<template>
	<div>
		<canvas ref="canvas" :width="width" :height="height"></canvas>
	</div>
</template>

<script>
	export default {
		name: 'Canvas',
		props: {
			width: {
				type: String,
				required: false,
				default: '1024px'
			},
			height: {
				type: String,
				required: false,
				default: '768px'
			}
		},
		data: () => ({
			ctx: null
		}),
		methods: {
			createContext() {
				this.ctx = this.$refs.canvas.getContext('2d');
			},
		},
		mounted() {
			this.createContext();
		},
	}
</script>