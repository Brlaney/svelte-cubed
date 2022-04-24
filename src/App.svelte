<script lang="ts">
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import Canvas from './components/Canvas.svelte';
	import PerspectiveCamera from './components/PerspectiveCamera.svelte';
	import Mesh from './components/Mesh.svelte';
	import AmbientLight from './components/AmbientLight.svelte';
	import DirectionalLight from './components/DirectionalLight.svelte';
	import Group from './components/Group.svelte';

	import { renderScene } from './lib/_scene';
	import { onFrame } from 'svelte-cubed';

	let container;
	$: container && renderScene(container);

	let intensity = 0.6;
	let intensity2 = 0.6;
	let x = -2;
	let spin = 0;

	onFrame(() => {
		spin += 0.01;
	});
</script>

<main>
	<!-- <div class='container' bind:this={container} /> -->
	<SC.Canvas background={new THREE.Color('papayawhip')}>
		<SC.PerspectiveCamera position={[1, 1, 3]} />
		<SC.Mesh
			geometry={new THREE.BoxGeometry()}
			material={new THREE.MeshStandardMaterial({ color: 0xff3e00 })}
			castShadow
			rotation={[0, spin, 0]}
		/>
		<SC.AmbientLight {intensity} />
		<SC.DirectionalLight intensity={intensity2} position={[x, 3, 2]} />
		<SC.Group>
			<SC.Mesh 
				geometry={new THREE.PlaneGeometry(50, 50)}
				material={new THREE.MeshStandardMaterial({ color: 'burlywood' })}
				rotation={[-Math.PI / 2, 0, 0]}
				receiveShadow
			/>
		</SC.Group>
	</SC.Canvas>
	<div class='bottom-row'>
		<input type='range' min={0} max={1} step={0.1} bind:value={intensity} />
		<input type='range' min={0} max={1} step={0.1} bind:value={intensity2} />
		<input type='range' min={-5} max={5} step={0.1} bind:value={x} />
	</div>
</main>

<style>
	main {
		/* height: 100%;
		width: 100vw; */
		padding: 0.5rem;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-content: center;
	}
	.container {
		width: 300px;
		height: 300px;
		margin: 0.2rem;
		outline: #040926 1px solid;
	}
	.bottom-row {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}
	input {
		margin: 0.1rem;
	}
</style>
