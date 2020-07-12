<template>
	<div class="parent">
		<div class="parent__name">{{ name }}</div>
		<button @click="addChild" class="btn parent__btn add-btn">+</button>
	</div>
</template>

<script>
	import uniqid from 'uniqid'

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
			}
		},
		methods: {
			addChild() {
				const child = {
					id: uniqid(),
					name: 'New child',
					parent: this.id,
					children: []
				};

				this.$emit('onAddChild', {child})
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