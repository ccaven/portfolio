<script lang="ts">
    import { T } from "@threlte/core";
	import { Text } from "@threlte/extras";

    export let name: string = "Unnamed";
</script>

<T.Group {...$$restProps}>

    <!-- Text -->
    <Text
        text="{name}"
        color="lightblue"
        fontSize={0.5}
        font="Hack-Regular.ttf"
        anchorX="50%"
        anchorY="0%"
        textAlign="center"
        position.y={2}
    />

    <T.Mesh position.y={-0.05}>

        <T.BoxGeometry args={[4, 0.1, 4]}/>
        <T.MeshStandardMaterial color="pink"/>

    </T.Mesh>

    <slot></slot>

</T.Group>