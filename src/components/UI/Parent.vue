<template>
	<div class="parent" :style="{top: position.y, left: position.x}">
		<div class="parent__name">{{ name }}</div>
		<button @click="addChild" class="btn parent__btn add-btn">+</button>
	</div>
</template>

<script>
	export default {
		name: 'Parent',
		props: {
			id: {
				type: String,
				required: true,
			},
			name: {
				type: String,
				required: false,
				default: 'New parent'
			},
			child: {
				type: Array,
				required: false,
				default: () => []
			},
			position: {
				type: Object,
				required: false,
				default: () => ({
					x: 0, y: 0
				})
			}
		},
		methods: {
			addChild(id) {
				this.child.push(id)
			}
		}
	}
</script>

<styles lang="scss">
	.parent {
		width: 100px;
		height: 100px;
		background: #ffcdbb;
	}
</styles>