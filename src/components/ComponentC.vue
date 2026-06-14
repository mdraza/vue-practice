<template>
    <h2>Component C</h2>
    <p>Full Name: {{ fullName }}</p>
</template>

<script>
    export default {
        name: "ComponentC",
        inject:["fullName"]
    }
</script>