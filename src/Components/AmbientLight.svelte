<script>
  import * as THREE from 'three';
  import { setup } from '../lib/context';
  
  export let color = 0xffffff;
  export let intensity = 1;

  const { root, item: light } = setup(new THREE.AmbientLight(color, intensity));

  $: {
    light.intensity = intensity;
    root.render();
  }

</script>
