<template>
	<Page class="canvas-wrapper">
		<ul>
			<li v-for="el in canvasElements" :key="el.id">
				<Parent
					v-if="el.children && el.children.length > 0"
					:id="el.id"
					:name="el.name"
					:position="el.position"
					:children="el.children"
					@onAddChild="addChildHandler(el.id, $event.child)"
					class="canvas-wrapper__item"
				/>
				<Child
					v-else
					:id="el.id"
					:name="el.name"
					:position="el.position"
					:parent="el.parent"
					class="canvas-wrapper__item"
				/>
			</li>
		</ul>
		<Canvas class="nodes-canvas"/>
	</Page>
</template>

<script>
	import Page from '../components/Page'
	import Canvas from '../components/UI/Canvas'
	import Parent from '../components/UI/Parent'
	import Child from '../components/UI/Child'

	import data from '../mocupData/data'

	export default {
		name: 'Main',
		components: {
			Page,
			Canvas,
			Parent,
			Child
		},
		data: () => ({
			canvasElements: []
		}),
		methods: {
			addChildHandler(id, child) {
				const canvasElements = [...this.canvasElements];
				const parent = canvasElements.filter(el => el.id === id)[0];
				const childCopy = {...child};

				childCopy.position = { x: 0, y: 0 };
				parent.children.push(child.id);
				canvasElements.push(child);

				this.canvasElements = canvasElements
			}
		},
		beforeMount() {
			const canvasElements = data.elements;

			this.canvasElements = canvasElements.map(el => ({
				...el,
				position: {
					x: 0, y: 0
				}
			}))
		}
	}
</script>

<style lang="scss">
	.canvas-wrapper {
		position: relative;
		&__item {
			position: absolute;
			z-index: 10;
		}

		ul {
			display: block;
			width: 100%;
			height: 100%;
			padding: 0;
			margin: 0;
			list-style: none;

			li {
				display: inline-block;
				padding: 0;
				margin: 0;
			}
		}

		canvas {
			position: absolute;
			top: 0;
			left: 0;
			z-index: 5;
		}
	}
</style>
