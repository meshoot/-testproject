<template>
	<Page class="canvas-wrapper">
		<div
			v-for="el in canvasElements"
			:key="el.id"
			@dragstart="() => false"
			@mousedown="mouseDownHandler"
		>
			<Parent
				v-if="el.children && el.children.length > 0"
				:id="el.id"
				:name="el.name"
				:children="el.children"
				:style="{top: el.position.y, left: el.position.x}"
				@onAddChild="addChildHandler(el.id, $event.child)"
				class="canvas-wrapper__item"
			/>
			<Child
				v-else
				:id="el.id"
				:name="el.name"
				:parent="el.parent"
				:style="{top: el.position.y, left: el.position.x}"
				class="canvas-wrapper__item"
			/>
		</div>
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
			mouseDownHandler(e) {
				const target = e.target;
				const shiftX = e.clientX - target.getBoundingClientRect().left;
				const shiftY = e.clientY - target.getBoundingClientRect().top;

				target.style.zIndex = 100;
				this.moveElement(target, { x: e.pageX - shiftX, y: e.pageY - shiftY });
				target.addEventListener('mousemove', e => {
					this.moveElement(target, {x: e.pageX, y: e.pageY})
				})
			},
			moveElement(el, coordinates) {
				const {x, y} = coordinates;

				el.style.left = `${x}px`;
				el.style.top = `${y}px`;
			},
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
			cursor: pointer;
		}

		canvas {
			position: absolute;
			top: 0;
			left: 0;
			z-index: 5;
		}
	}
</style>
