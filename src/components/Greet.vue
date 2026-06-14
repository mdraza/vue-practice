<template>
  <h2>Hi...{{ name }} {{ lname }}</h2>
</template>

<script>
export default {
  name: "Greet",
  props: ["name", "lname"],
};
</script>

<style></style>
