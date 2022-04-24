<script>
  import * as THREE from 'three';
  import { setup } from '../lib/context';
  import { getContext } from 'svelte';
  
  export let position = [0, 0, 0];

  const camera = new THREE.PerspectiveCamera(45, 1, 0.1, 2000);
  camera.position.x = position[0];
  camera.position.y = position[1];
  camera.position.z = position[2];
  camera.lookAt(new THREE.Vector3(0, 0, 0))

  const canvasRoot = getContext(CANVAS);
  canvasRoot.camera = camera;
  canvasRoot.render();
</script>
