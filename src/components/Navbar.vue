<script setup>
    import logo from '@/assets/images/logo.png'
</script>

<template>
    <nav class="navbar navbar-expand-md navbar-dark bg-success border-bottom border-success">
        <div class="container">
            <!-- Logo -->
            <a class="navbar-brand d-flex align-items-center" href="index.html">
            <img :src="logo" alt="Vue Jobs" class="me-2" height="40">
            <span class="d-none d-md-block fs-4 fw-bold">Vue Jobs</span>
            </a>
            
            <!-- Navbar toggler for mobile -->
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
            </button>

            <!-- Navbar links -->
            <div class="collapse navbar-collapse justify-content-md-end" id="navbarNav">
            <ul class="navbar-nav">
                <li class="nav-item">
                <a class="nav-link active bg-dark rounded px-3 py-2" href="index.html">Home</a>
                </li>
                <li class="nav-item">
                <a class="nav-link text-white rounded px-3 py-2" href="jobs.html">Jobs</a>
                </li>
                <li class="nav-item">
                <a class="nav-link text-white rounded px-3 py-2" href="add-job.html">Add Job</a>
                </li>
            </ul>
            </div>
        </div>
    </nav>

</template>
