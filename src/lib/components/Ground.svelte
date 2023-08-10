<script lang="ts">
    import { T } from '@threlte/core';
    import { Grid } from '@threlte/extras';
    import { AutoColliders, Collider } from "@threlte/rapier";
    import { Text } from '@threlte/extras';
</script>

<T.Group position.y={-1}>
    <Collider shape="cuboid" args={[100, 1, 100]} friction={999}/>
</T.Group>

<T.Group>
    <AutoColliders shape="convexHull" friction={999}>

        <T.Mesh position.y={-2}>

            <T.IcosahedronGeometry args={[4, 3]}/>
            <T.MeshStandardMaterial color="purple" flatShading/>

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

<T.Group position.z={10} rotation.x={-Math.PI/2}>
    <Text
        text={"    ⬆\n    w\n⬅ a   d ➡\n    s\n    ⬇"}
        color="lightblue"
        fontSize={1}
        font="Hack-Regular.ttf"
        anchorX="50%"
        anchorY="50%"
    />
</T.Group>

<T.Group position.z={13.5} rotation.x={-Math.PI/2}>
    <Text
        text={"welcome to xacer.dev\n\ni make magic at the intersection\nof 3D and AI"}
        color="lightblue"
        fontSize={0.5}
        font="Hack-Regular.ttf"
        anchorX="50%"
        anchorY="0%"
        textAlign="center"
    />
</T.Group>

<T.Group position.z={-7}>

    <!-- local constant -->
    {@const rampWidth = 3}

    <T.Group rotation.x={Math.acos(1 / rampWidth)}>
        <AutoColliders shape="cuboid">
            <T.Mesh>
                <T.BoxGeometry args={[2, rampWidth, 1]}/>
                <T.MeshStandardMaterial color="orange" />
            </T.Mesh>
        </AutoColliders>
    </T.Group>

</T.Group>


