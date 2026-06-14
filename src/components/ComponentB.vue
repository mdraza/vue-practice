<template>
    <h2>Component B</h2>
    <ComponentC/>
</template>

<script>
import ComponentC from './ComponentC.vue';

    export default {
        name: "ComponentB",
        components: {
            ComponentC,
        }
    }
</script>