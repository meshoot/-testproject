<template>
	<div>
		<h1 v-if="title">{{ title }}</h1>
		<slot/>
	</div>
</template>

<script>
	export default {
		name: 'Page',
		props: {
			title: {
				type: String,
				required: false
			}
		},
		components: {

		}
	}
</script>
