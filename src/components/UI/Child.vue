<template>
	<div class="child">
		<div class="child__name">{{ name }}</div>
		<button @click="removeParent" class="btn child__btn remove-btn">-</button>
	</div>
</template>

<script>
	export default {
		name: 'Child',
		props: {
			id: {
				type: String,
				required: true,
			},
			name: {
				type: String,
				required: false,
				default: 'New child'
			},
			parent: {
				type: String,
				required: false,
			}
		},
		methods: {
			removeParent() {
				this.parent = null;
			}
		}
	}
</script>

<styles lang="scss">
	.child {
		width: 50px;
		height: 50px;
		background: #bbffcf;
	}
</styles>