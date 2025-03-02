<script setup>
import logo from '@/assets/images/logo.png'
import { RouterLink, useRoute } from 'vue-router'
import { ref } from 'vue';

const hover = ref(false)
const isActiveLink = (routePath) => {
    const route = useRoute();
    return route.path === routePath;
}
</script>

<template>
    <nav class="navbar navbar-expand-md navbar-dark bg-success border-bottom border-success">
        <div class="container">
            <!-- Logo -->
            <RouterLink class="navbar-brand d-flex align-items-center" to="/">
                <img :src="logo" alt="Vue Jobs" class="me-2" height="40">
                <span class="d-none d-md-block fs-4 fw-bold">Vue Jobs</span>
            </RouterLink>
            
            <!-- Navbar toggler for mobile -->
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
            </button>

            <!-- Navbar links -->
            <div class="collapse navbar-collapse justify-content-md-end" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item">
                    <RouterLink class="nav-link active bg-dark rounded px-3 py-2" to="/">Home</RouterLink>
                </li>
                <li class="nav-item">
                    <RouterLink class="nav-link text-white rounded px-3 py-2" to="/jobs">Jobs</RouterLink>
                </li>
                <li class="nav-item">
                    <RouterLink class="nav-link text-white rounded px-3 py-2" to="/jobs/add">Add Job</RouterLink>
                </li>
            </ul>
            </div>
        </div>
    </nav>

</template>
