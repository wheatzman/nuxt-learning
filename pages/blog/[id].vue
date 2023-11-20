<template>
    <div>
        We are inside the Blog
    </div>
    <div>
        Blog entry {{ route.params.id }}
    </div>
</template>

<script setup>
const route = useRoute();
</script>