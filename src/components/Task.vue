<template>
  <div class="task">
    <div class="row">
      <div class="col-sm">
        <form class="form-group">
          <input
            type="text"
            class="form-control input"
            :placeholder="task.title"
          />
        </form>
      </div>
      <div class="col-">
        <button type="button" class="btn btn-danger" @click="emitDelete">
          <font-awesome-icon icon="trash" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["task"],
  methods: {
    emitDelete() {
      this.$emit("taskEmitted", this.task);
    }
  }
};
</script>

<style lang="sass">
.task
    text-align: center
</style>
