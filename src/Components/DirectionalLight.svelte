<script>
  import * as THREE from 'three';
  import { setup } from '../lib/context';

  export let color = 0xffffff;
  export let intensity;
  export let position = [0, 0, 0];
  export let targetPosition = [0, 0, 0];

  const { root, item: directionalLight } = setup(new THREE.DirectionalLight());

  $: {
    directionalLight.intensity = intensity;
    directionalLight.color.set(color);
    directionalLight.position.set(position[0], position[1], position[2]);
    directionalLight.castShadow = true;
    directionalLight.target.position.set(
      targetPosition[0],
      targetPosition[1],
      targetPosition[2]
    );
    root.render();
  }
</script>
