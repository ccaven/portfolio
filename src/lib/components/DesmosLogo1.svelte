<!--
Auto-generated by: https://github.com/threlte/threlte/tree/main/packages/gltf
Command: npx @threlte/gltf@1.0.1 ./static/desmos-logo-1.glb
-->

<script>
  import { Group } from 'three'
  import { T, forwardEventHandlers } from '@threlte/core'
  import { useGltf } from '@threlte/extras'

  export const ref = new Group()

  const gltf = useGltf('/desmos-logo-1.glb')

  const component = forwardEventHandlers()
</script>

<T is={ref} dispose={false} {...$$restProps} bind:this={$component}>
  {#await gltf}
    <slot name="fallback" />
  {:then gltf}
    <T.Group rotation={[Math.PI / 2, 0, 0]}>
      <T.Mesh geometry={gltf.nodes['icons8-desmos-200_1'].geometry} material={gltf.materials['icons8-desmos-200']} />
      <T.Mesh geometry={gltf.nodes['icons8-desmos-200_2'].geometry} material={gltf.materials['Material.001']} />
      <T.Mesh geometry={gltf.nodes['icons8-desmos-200_3'].geometry} material={gltf.materials['Material.002']} />
    </T.Group>
  {:catch error}
    <slot name="error" {error} />
  {/await}

  <slot {ref} />
</T>
