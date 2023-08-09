<script lang="ts">
    import { T } from '@threlte/core';
    import { Grid, OrbitControls } from '@threlte/extras';
    import { AutoColliders, Collider, RigidBody } from "@threlte/rapier";
	import { MeshStandardMaterial, TetrahedronGeometry } from 'three';

    import { Text } from '@threlte/extras';
</script>

<T.Group position.y={-1}>
    <Collider shape="cuboid" args={[100, 1, 100]} friction={999}/>
</T.Group>

<T.Group>
    <AutoColliders shape="convexHull" friction={999}>

        <T.Mesh position.y={-2}>

            <T.IcosahedronGeometry args={[4, 3]}/>
            <T.MeshStandardMaterial color="red" flatShading/>

        </T.Mesh>

    </AutoColliders>
</T.Group>

<Grid
  position.y={-0.001}
  cellColor="#ffffff"
  sectionColor="#ffffff"
  sectionThickness={0}
  fadeDistance={50}
  cellSize={2}
  gridSize={100}
/>

<T.Group position.z={7} rotation.x={-Math.PI/2}>
    <Text
    text={"xacer.dev\nhello there"}
    color="lightblue"
    fontSize={1}
    anchorX="50%"
    anchorY="50%"
/>
</T.Group>
