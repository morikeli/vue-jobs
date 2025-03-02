<script setup>
import { defineProps, ref, computed } from 'vue'
import { RouterLink } from 'vue-router'

const props = defineProps({
    job: Object,
})

const showFullDescription = ref(false)

const toggleFullDescription = () => {
    showFullDescription.value = !showFullDescription.value
}

const truncatedDescription = computed(() => {
    let description = props.job.description

    if (!showFullDescription.value) {
        description = description.substring(0, 90) + '...'
    }

    return description
})
</script>

<template>
    <div class="col-md-4">
        <div class="card h-100 shadow flex-fill">
          <div class="card-body">
            <div class="text-muted">{{ job.type }}</div>
            <h3 class="h5 fw-bold">{{ job.title }}</h3>
            <div class="mb-3">
                <div>
                    {{ truncatedDescription }}
                </div>
                <button @click="toggleFullDescription" class="btn text-success text-opacity-75">{{ showFullDescription ? 'Less' : 'Read more'}}</button>
            </div>
            <h3 class="text-success">{{ job.salary }}</h3>
            <hr>
            <div class="d-flex justify-content-between align-items-center">
              <span class="text-secondary"><i class="pi pi-map-marker"></i> {{ job.location }}</span>
              <RouterLink :to="'/jobs/' + job.id" class="btn btn-success btn-sm">Read More</RouterLink>
            </div>
          </div>
        </div>
    </div>
</template>
