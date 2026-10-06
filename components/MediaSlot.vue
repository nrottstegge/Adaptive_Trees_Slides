<script setup>
import { ref, watch } from 'vue'
// Image / GIF from public/ with a placeholder fallback until the file exists.
const props = defineProps({
  src: { type: String, default: '' },
  label: { type: String, default: '[INSERT SCREENSHOT]' },
  note: { type: String, default: '' },
  fit: { type: String, default: 'contain' },
})
const failed = ref(!props.src)
watch(() => props.src, s => { failed.value = !s })
</script>

<template>
  <div class="media">
    <img v-if="!failed" :src="src" :style="{ objectFit: fit }" @error="failed = true" />
    <Placeholder v-else :label="label" :note="note || (src ? `put file at public${src}` : '')" h="100%" />
  </div>
</template>

<style scoped>
.media { width: 100%; height: 100%; position: relative; }
img { position: absolute; inset: 0; width: 100%; height: 100%; }
</style>
