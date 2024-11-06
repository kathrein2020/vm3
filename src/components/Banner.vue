
<script setup>
const {banner} = defineProps(["banner"])
</script>

<template>
<!-- обращение к :banner = "bannerMovie" в template, что обращается к  -->
    <p>{{banner}}</p>
    <h1>{{ banner.title }}</h1>

    
    </template>
    