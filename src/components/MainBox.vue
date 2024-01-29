<template>
  <div class="container">
    <Nav></Nav>
    <TaskTextBox></TaskTextBox>
  </div>
</template>

<script setup>
import Nav from "./Nav.vue";
import TaskTextBox from "./TaskTextBox.vue";
</script>
<style scoped>
.container {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 400px;
  height: 600px;
  position: absolute;
  border: 1px solid black;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 10px;
}
</style>
