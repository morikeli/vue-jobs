<script setup>
    import { defineProps } from 'vue'

    defineProps({
        title: {
            type:    String,
            default: 'Be a Vue dev',
        },
        subtitle: {
            type:    String,
            default: 'Find the Vue job that fits your skills and needs',
        },
    })
</script>

<template>
    <section class="bg-success py-5 mb-4 text-center">
  <div class="container">
    <h1 class="display-4 fw-bold text-white">{{ title }}</h1>
    <p class="lead text-white">{{ subtitle }}</p>
  </div>
</section>
</template>
