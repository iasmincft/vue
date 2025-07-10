<template>
    <div class="container">
        <h1 class="emphasized">{{page.pageTitle}}</h1>
        <p>{{page.content}}</p>
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