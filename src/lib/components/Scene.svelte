<script lang="ts">
    import { T } from '@threlte/core';
    import { Grid, OrbitControls } from '@threlte/extras';
    import { AutoColliders, Collider, Debug, RigidBody } from "@threlte/rapier";
	import Ground from './Ground.svelte';
	import Player from './Player.svelte';
	import Exhibit from './Exhibit.svelte';
	import Center from './Center.svelte';
</script>


<T.DirectionalLight intensity={0.8} position.x={5} position.y={10} />
<T.AmbientLight intensity={0.2} />

<Ground />
<Center />
<Player />

<Exhibit name="Code Together" position.x={20} position.z={-10}>

</Exhibit>

<Exhibit name="Multiplayer Desmos" position.x={20} position.z={10}>

</Exhibit>

<Exhibit name="Black hole raytracing" position.x={-20} position.z={-10}>

</Exhibit>

<Exhibit name="AI research" position.x={-20} position.z={10}>

</Exhibit>

<!--
<Float floatIntensity={1} floatingRange={[0, 1]} >
  <T.Mesh position.y={1.2} position.z={-0.75}>
    <T.BoxGeometry />
    <T.MeshStandardMaterial color="#0059BA" />
  </T.Mesh>
</Float>

<Float floatIntensity={1} floatingRange={[0, 1]}>
  <T.Mesh position={[1.2, 1.5, 0.75]} rotation.x={5} rotation.y={71}>
    <T.TorusKnotGeometry args={[0.5, 0.15, 100, 12, 2, 3]} />
    <T.MeshStandardMaterial color="#F85122" />
  </T.Mesh>
</Float>

<Float floatIntensity={1} floatingRange={[0, 1]}>
  <T.Mesh position={[-1.4, 1.5, 0.75]} rotation={[-5, 128, 10]}>
    <T.IcosahedronGeometry />
    <T.MeshStandardMaterial color="#F8EBCE" />
  </T.Mesh>
</Float>
-->