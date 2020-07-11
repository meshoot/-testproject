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
			createRect(params, type) {
				if (!params) {
					return new Error('Parameters not specified for drawing')
				}

				const { x, y, width, height, fill, stroke } = params;

				if (type === 'fill') {
					this.ctx.fillRect(x, y, width, height);
					if (fill) {
						this.ctx.fillStyle = fill;
					}
				} else {
					this.ctx.strokeRect(x, y, width, height);
					if (stroke) {
						this.ctx.strokeStyle = stroke;
					}
				}
			},
			clearRect(params) {
				if (!params) {
					return new Error('Parameters not specified for drawing')
				}

				const { x, y, width, height } = params;

				this.ctx.clearRect(x, y, width, height)
			}
		},
		mounted() {
			this.createContext();
		},
	}
</script>