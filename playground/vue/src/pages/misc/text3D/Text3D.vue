<script setup lang="ts">
import { extend, useTexture } from '@tresjs/core'
import { TextGeometry } from 'three/examples/jsm/geometries/TextGeometry'
import { FontLoader } from 'three/examples/jsm/loaders/FontLoader'

const props = defineProps<{
  text: string
}>()

extend({ TextGeometry })

const fontPath = 'https://raw.githubusercontent.com/Tresjs/assets/main/fonts/FiraCodeRegular.json'

const fontOptions = {
  size: 0.5,
  height: 0.2,
  curveSegments: 5,
  bevelEnabled: true,
  bevelThickness: 0.02,
  bevelSize: 0.02,
  bevelOffset: 0,
  bevelSegments: 4,
}

const loader = new FontLoader()

const font = await new Promise((resolve, reject) => {
  try {
    loader.load(fontPath, (font) => {
      resolve(font)
    })
  }
  catch (error) {
    reject(console.error('cientos', error))
  }
})

const matcapTexture = await useTexture(['https://raw.githubusercontent.com/Tresjs/assets/main/textures/matcaps/7.png'])
</script>

<template>
  <TresMesh>
    <TresTextGeometry
      :args="[props.text, { font, ...fontOptions }]"
      center
    />
    <TresMeshNormalMaterial :matcap="matcapTexture" />
  </TresMesh>
</template>
