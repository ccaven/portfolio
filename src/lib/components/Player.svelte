<script lang="ts">
    import type { RigidBody as RapierRigidBody } from "@dimforge/rapier3d-compat";
    import { Vector3, type PerspectiveCamera, type Group } from "three";
    import type { OrbitControls as ThreeOrbitControls } from 'three/examples/jsm/controls/OrbitControls';
    
    import { T, useFrame, useThrelte } from '@threlte/core';
	import { OrbitControls } from '@threlte/extras';
    import { AutoColliders, RigidBody } from "@threlte/rapier";
	import { onMount } from "svelte";

    let rigidBody: RapierRigidBody;
    let perspectiveCamera: PerspectiveCamera;
    let cameraGroup: Group;
    let orbitControls: ThreeOrbitControls;

    let { renderer } = useThrelte();

    let pressedKeys: { [key: string]: boolean } = {};

    let speed = 0.5;
    let dragSpeed = 0.01;

    onMount(() => {
        window.addEventListener("keydown", event => {pressedKeys[event.key] = true; console.log(event.key)});
        window.addEventListener("keyup", event => pressedKeys[event.key] = false);
    });

    useFrame((_, delta) => {

        if (!rigidBody || !perspectiveCamera) return;

        let rigidBodyPosition = rigidBody.translation();
        let velocity = rigidBody.linvel();

        orbitControls.target.set(rigidBodyPosition.x, rigidBodyPosition.y, rigidBodyPosition.z);
        perspectiveCamera.position.add(new Vector3(velocity.x * delta, velocity.y * delta, velocity.z * delta));

        let zAxis = orbitControls.target.clone().sub(perspectiveCamera.position).setY(0).normalize();
        let xAxis = zAxis.clone().cross(new Vector3(0, 1, 0));

        let torque = new Vector3();

        if (pressedKeys["w"] || pressedKeys["ArrowUp"]) torque.sub(xAxis);
        if (pressedKeys["s"] || pressedKeys["ArrowDown"]) torque.add(xAxis);
        if (pressedKeys["a"] || pressedKeys["ArrowLeft"]) torque.sub(zAxis);
        if (pressedKeys["d"] || pressedKeys["ArrowRight"]) torque.add(zAxis);

        if (torque.lengthSq() > 0.1) {
            torque.normalize().multiplyScalar(speed * delta);
            rigidBody.applyTorqueImpulse(torque, true);
        }

        // execute damping
        let angvel = rigidBody.angvel();
        if (angvel.x * angvel.x + angvel.y * angvel.y + angvel.z * angvel.z > 0.1 * 0.1) {
            rigidBody.applyTorqueImpulse({
                x: -angvel.x * dragSpeed * delta,
                y: -angvel.y * dragSpeed * delta,
                z: -angvel.z * dragSpeed * delta
            }, true);
        }

    });

</script>



<T.Group position.y={10}>
    <RigidBody bind:rigidBody={rigidBody}>
        <AutoColliders shape="ball">
            <T.Mesh>
                <T.SphereGeometry args={[0.25]}/>
                <T.MeshStandardMaterial/>                
            </T.Mesh>
        </AutoColliders>
    </RigidBody>
</T.Group>

<T.Group bind:ref={cameraGroup}>
    <T.PerspectiveCamera makeDefault position={[-5, 5, 5]} fov={60} bind:ref={perspectiveCamera}>
        <OrbitControls
            autoRotate 
            enableZoom={false} 
            enableDamping
            autoRotateSpeed={0.1}
            maxPolarAngle={Math.PI * 5 / 8}
            minPolarAngle={Math.PI / 8}
            bind:ref={orbitControls}
        />
    </T.PerspectiveCamera>
</T.Group>