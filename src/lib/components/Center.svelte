<script lang="ts">
    import { T } from '@threlte/core';
    import { AutoColliders, Collider } from "@threlte/rapier";
</script>

<T.Group>
    <AutoColliders shape="convexHull" friction={999}>

        <T.Mesh position.y={0}>

            <T.IcosahedronGeometry args={[2, 2]}/>
            <T.MeshStandardMaterial color="purple" flatShading/>

        </T.Mesh>

    </AutoColliders>
</T.Group>

{#each [0, 1, 2, 3] as i}


    {@const angle = (i + 0.5) * Math.PI / 2}
    <T.Group rotation.y={angle}>
        <T.Group position.z={-5}>

            <!-- local constant -->
            {@const rampWidth = 4}

            <T.Group rotation.x={Math.acos(1 / rampWidth)}>
                <AutoColliders shape="cuboid">
                    <T.Mesh>
                        <T.BoxGeometry args={[2, rampWidth, 1]}/>
                        <T.MeshStandardMaterial color="orange" />
                    </T.Mesh>
                </AutoColliders>
            </T.Group>

        </T.Group>
    </T.Group>

{/each}