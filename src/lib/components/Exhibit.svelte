<script lang="ts">
    import { T } from "@threlte/core";
	import { Text, interactivity } from "@threlte/extras";
	import DesmosLogo1 from "./DesmosLogo1.svelte";

    export let name: string = "Unnamed";

    interactivity();


    type InteractivityEvent = THREE.Intersection & {
        intersections: THREE.Intersection[] // The first intersection of each intersected object
        object: THREE.Object3D // The object that was actually hit
        eventObject: THREE.Object3D // The object that registered the event
        camera: THREE.Camera // The camera used for raycasting
        delta: THREE.Vector2 //  Distance between mouse down and mouse up event in pixels
        nativeEvent: MouseEvent | PointerEvent | WheelEvent // The native browser event
        pointer: THREE.Vector2 // The pointer position in normalized device coordinates
        ray: THREE.Ray // The ray used for raycasting
        stopPropagation: () => void // Function to stop propagation of the event
        stopped: Boolean // Whether the event propagation has been stopped
    }

    function onPointerOver(event: InteractivityEvent) {

        event.object.scale.setScalar(1.1);

    }
    function onPointerOut(event: InteractivityEvent) {

        
        event.object.scale.setScalar(1.0);

    }
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
        position.y={1.75}
    />

    <T.Mesh position.y={-0.05} on:pointerover={onPointerOver} on:pointerout={onPointerOut}>

        <T.BoxGeometry args={[4, 0.1, 4]}/>
        <T.MeshStandardMaterial color="pink"/>

    </T.Mesh>

    <DesmosLogo1 position.y={2.5} scale={2}/>

    <slot></slot>

</T.Group>