<script setup>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import axios from 'axios'
import { reactive, onMounted } from 'vue'
import { useRoute, RouterLink, useRouter } from 'vue-router'
import BackButton from '@/components/BackButton.vue'
import { useToast } from 'vue-toastification'

const route = useRoute()
const router = useRouter()
const toast = useToast()
const jobId = route.params.id

const state = reactive({
    job: {},
    isLoading: true,
})

const deleteJob  = async () => {
    try {
        const confirm = window.confirm('Are you sure you want to delete this job?')     // prompt user if they want to delete the job
        // if the user has confirmed he wants to delete the job, delete it.
        if (confirm) {
            await axios.delete(`/api/jobs/${jobId}`)
            toast.success('Job deleted successfully!')
            router.push('/jobs')
        }
        
    } catch (err) {
        console.error('Error deleting job', err)
        toast.error('Job not deleted.')
    }
}

onMounted(async () => {
    try {
        const response = await axios.get(`/api/jobs/${jobId}`)
        state.job = response.data
    } catch (err) {
        console.error('Error fetching job', err)
    } finally {
        state.isLoading = false;
    }
})
</script>

<template>
    <BackButton />
    <section v-if="!state.isLoading" class="bg-light my-4">
        <div class="container py-10 px-6">
            <div class="row g-4">
                <main class="col-md-8">
                    <div class="bg-white p-4 rounded shadow text-center text-md-start">
                        <div class="text-muted mb-3">{{ state.job.type }}</div>
                        <h1 class="h2 fw-bold mb-3">{{ state.job.title }}</h1>
                        <div class="text-muted d-flex justify-content-center justify-content-md-start align-items-center mb-3">
                            <i class="pi pi-map-marker text-danger me-2"></i>
                            <p class="text-danger mb-0">{{ state.job.location }}</p>
                        </div>
                    </div>

                    <div class="bg-white p-4 rounded shadow mt-4">
                        <h3 class="text-success fw-bold mb-4">Job Description</h3>
                        <p>
                            {{ state.job.description }}
                        </p>

                        <h3 class="text-success fw-bold mb-2">Salary</h3>
                        <p>{{ state.job.salary }} / Year</p>
                    </div>
                </main>

                <!-- Sidebar -->
                <aside class="col-md-4">
                    <div class="bg-white p-4 rounded shadow">
                        <h3 class="h4 fw-bold mb-4">Company Info</h3>
                        <h2 class="h5">{{ state.job.company.name }}</h2>
                        <p class="my-2">
                            {{ state.job.company.description }}
                        </p>

                        <hr class="my-3" />

                        <h3 class="h5">Contact Email:</h3>
                        <p class="my-2 bg-success text-white p-2 fw-bold rounded">{{ state.job.company.contactEmail }}</p>

                        <h3 class="h5">Contact Phone:</h3>
                        <p class="my-2 bg-success text-white p-2 fw-bold rounded">{{ state.job.company.contactPhone }}</p>
                    </div>

                    <!-- Manage Job -->
                    <div class="bg-white p-4 rounded shadow mt-4">
                        <h3 class="h4 fw-bold mb-4">Manage Job</h3>
                        <RouterLink :to="`/jobs/${state.job.id}/edit`" class="btn btn-success w-100 mb-3">Edit Job</RouterLink>
                        <button class="btn btn-danger w-100" @click="deleteJob">Delete Job</button>
                    </div>
                </aside>
            </div>
        </div>
    </section>

    <!-- Loading spinner -->
    <div v-else class="my-4 text-center text-secondary py-6">
        <PulseLoader/>
    </div>
</template>
