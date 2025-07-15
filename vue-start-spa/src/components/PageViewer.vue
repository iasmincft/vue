<template>
    <div class="container">
        <h1 class="emphasized">Page Title</h1>
        <p>Content </p>
    </div>
</template>

<script>
    export default {
        props: ['page']
    }
</script>

<style scoped>
    .emphasized {
        color: blue;
    }
</style>