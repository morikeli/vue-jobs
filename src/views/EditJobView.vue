<script setup>
import { reactive, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import router  from '@/router';
import axios from 'axios';
import { useToast } from 'vue-toastification';


const route = useRoute()
const jobId = route.params.id
const form = reactive({
    type: 'Full-Time',
    title: '',
    description: '',
    salary: '',
    location: '',
    company: {
        name: '',
        description: '',
        contactEmail: '',
        contactPhone: '',
    }
})

const state = reactive({
    job: {},
    isLoading: true,
})
const toast = useToast()

const handleSubmit = async () => {
    const updateJob = {
        title: form.title,
        type: form.type,
        location: form.location,
        description: form.description,
        salary: form.salary,
        company: {
            name:form.company.name,
            description: form.company.description,
            contactEmail: form.company.contactEmail,
            contactPhone: form.company.contactPhone,
        }
    }
    
    try {
        const response = await axios.put(`/api/jobs/${jobId}`, updateJob)
        toast.success('Job updated successfully!')
        router.push(`/jobs/${response.data.id}`)
    } catch (err) {
        toast.error("Job couldn't be added")
        console.error('Error creating job', err)
    }
}

onMounted(async () => {
    try {
        const response = await axios.get(`/api/jobs/${jobId}`)
        state.job = response.data
        
        // populate form inputs
        form.type  = state.job.type
        form.title = state.job.title
        form.description = state.job.description
        form.salary = state.job.salary
        form.location = state.job.location
        form.company.name = state.job.company.name
        form.company.description = state.job.company.description
        form.company.contactEmail = state.job.company.contactEmail
        form.company.contactPhone = state.job.company.contactPhone

    } catch (err) {
        console.error('Error fetching job', err)
    } finally {
        state.isLoading = false;
    }
})
</script>
<template>
    <section class="bg-light">
        <div class="container py-5">
            <div class="mx-auto bg-white p-4 p-md-5 shadow-sm rounded border" style="max-width: 600px;">
                <form @submit.prevent="handleSubmit">
                    <h2 class="text-center fw-semibold mb-4">Edit Job</h2>

                    <!-- Job Type -->
                    <div class="mb-3">
                        <label for="type" class="form-label fw-bold">Job Type</label>
                        <select v-model="form.type" id="type" name="type" class="form-select" required>
                            <option value="Full-Time">Full-Time</option>
                            <option value="Part-Time">Part-Time</option>
                            <option value="Remote">Remote</option>
                            <option value="Internship">Internship</option>
                        </select>
                    </div>

                    <!-- Job Listing Name -->
                    <div class="mb-3">
                        <label for="name" class="form-label fw-bold">Job Listing Name</label>
                        <input v-model="form.title" type="text" id="name" name="name" class="form-control" placeholder="e.g., Senior Vue Developer" required>
                    </div>

                    <!-- Job Description -->
                    <div class="mb-3">
                        <label for="description" class="form-label fw-bold">Description</label>
                        <textarea v-model="form.description" id="description" name="description" class="form-control" rows="4" placeholder="Add job duties, expectations, etc"></textarea>
                    </div>

                    <!-- Salary -->
                    <div class="mb-3">
                        <label for="salary" class="form-label fw-bold">Salary</label>
                        <select v-model="form.salary" id="salary" name="salary" class="form-select" required>
                            <option value="Under $50K">Under $50K</option>
                            <option value="$50K - $60K">$50K - $60K</option>
                            <option value="$60K - $70K">$60K - $70K</option>
                            <option value="$70K - $80K">$70K - $80K</option>
                            <option value="$80K - $90K">$80K - $90K</option>
                            <option value="$90K - $100K">$90K - $100K</option>
                            <option value="$100K - $125K">$100K - $125K</option>
                            <option value="$125K - $150K">$125K - $150K</option>
                            <option value="$150K - $175K">$150K - $175K</option>
                            <option value="$175K - $200K">$175K - $200K</option>
                            <option value="Over $200K">Over $200K</option>
                        </select>
                    </div>

                    <!-- Location -->
                    <div class="mb-3">
                        <label for="location" class="form-label fw-bold">Location</label>
                        <input v-model="form.location" type="text" id="location" name="location" class="form-control" placeholder="Company Location" required>
                    </div>

                    <!-- Company Info Section -->
                    <h3 class="h4 mb-3">Company Info</h3>

                    <!-- Company Name -->
                    <div class="mb-3">
                        <label for="company" class="form-label fw-bold">Company Name</label>
                        <input v-model="form.company.name" type="text" id="company" name="company" class="form-control" placeholder="Company Name">
                    </div>

                    <!-- Company Description -->
                    <div class="mb-3">
                        <label for="company_description" class="form-label fw-bold">Company Description</label>
                        <textarea v-model="form.company.description" id="company_description" name="company_description" class="form-control" rows="4" placeholder="What does your company do?"></textarea>
                    </div>

                    <!-- Contact Email -->
                    <div class="mb-3">
                        <label for="contact_email" class="form-label fw-bold">Contact Email</label>
                        <input v-model="form.company.contactEmail" type="email" id="contact_email" name="contact_email" class="form-control" placeholder="Email address for applicants" required>
                    </div>

                    <!-- Contact Phone -->
                    <div class="mb-4">
                        <label for="contact_phone" class="form-label fw-bold">Contact Phone</label>
                        <input v-model="form.company.contactPhone" type="tel" id="contact_phone" name="contact_phone" class="form-control" placeholder="Optional phone for applicants">
                    </div>

                    <!-- Submit Button -->
                    <div>
                        <button type="submit" class="btn btn-success w-100">Edit Job</button>
                    </div>
                </form>
            </div>
        </div>
    </section>
</template>
