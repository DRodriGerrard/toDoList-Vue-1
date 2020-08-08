<template>
  <div class="home">
    <ToDoList />
  </div>
</template>

<script>
// @ is an alias to /src
import ToDoList from "@/components/ToDoList.vue";

require("../assets/styles/Home.sass");

export default {
  name: "Home",
  components: {
    ToDoList
  }
};
</script>
