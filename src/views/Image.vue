<template>
    <base-layout header-title="Image">
        <slide-001 />
    </base-layout>
</template>

<script lang="ts">
import slide001 from '@/components/slides/slide001.vue'
import { defineComponent } from 'vue'

export default defineComponent({
  components: { slide001 },
    setup () {
        return {}
    }
})
</script>

<style scoped>

</style>