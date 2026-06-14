<template>
    <h2>Component A</h2>
    <ComponentB/>
</template>

<script>
import ComponentB from './ComponentB.vue';

    export default {
        name: "ComponentA",
        components: {
            ComponentB,
        }
    }
</script>