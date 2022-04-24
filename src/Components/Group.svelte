<script>
  import * as THREE from 'three';
  import { setup } from '../lib/context';

  const { item: group } = setup(new THREE.Group());
  group.position.set(0, -0.5, 0);
</script>

<slot />
