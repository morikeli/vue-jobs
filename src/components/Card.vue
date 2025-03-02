<script setup>
    import { defineProps } from 'vue'

    defineProps({
        bg: {
            type: String,
            default: 'bg-light'
        }
    })
</script>
<template>
    <div :class="`${bg} p-4 rounded shadow h-100`">
        <slot></slot>
    </div>
</template>
