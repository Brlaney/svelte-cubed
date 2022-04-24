<script>
  import * as THREE from 'three';
  import { setup } from '../lib/context';

  export let geometry;
  export let material;
  export let rotation = [0, 0, 0];
  export let receiveShadow = false;
  export let castShadow = false;

  const { root, item: box } = setup(new THREE.Mesh(geometry, material));

  $: {
    box.rotation.set(rotation[0], rotation[1], rotation[2]);
    box.receiveShadow = receiveShadow;
    box.castShadow = castShadow;
    root.render();
  }
</script>

