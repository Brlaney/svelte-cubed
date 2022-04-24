<script>
	import * as THREE from 'three';
	// import * as SC from 'svelte-cubed';
	import { onMount, setContext } from 'svelte';
  import { CANVAS } from '../lib/context';

	let container;
	export let background;
	let scene;

	let canvasRoot = {
		scene,
		camera: undefined,
		renderer: undefined,
		render() {
			canvasRoot.renderer.render(canvasRoot.scene, canvasRoot.camera);
		}
	};

	setContext(CANVAS, canvasRoot);

	onMount(() => {
		scene = new THREE.Scene();
		scene.background = background;

		const renderer = new THREE.WebGLRenderer();
		renderer.setSize(container.clientWidth, container.clientHeight);
		container.appendChild(renderer.domElement);

		canvasRoot.scene = scene;
		canvasRoot.renderer = renderer;

		renderer.shadowMap.enabled = true;
		renderer.shadowMap.autoUpdate = true;
		renderer.shadowMap.type = THREE.PCFShadowMap;
	});

	$: {
		if (scene) {
			// TODO: Duplicated code over here
			scene.background;
		}
		// Redraws the scene
	}
</script>

<div class='container' bind:this={container} />

{#if scene}
	<slot />
{/if}

<style>
	.container {
		width: 300px;
		height: 300px;
		margin: 0.2rem;
		outline: #040926 1px solid;
	}
</style>
