<template>
  <div class="task">
    <div class="row">
      <div class="col-sm">
        <form class="form-group">
          <input
            type="text"
            class="form-control input"
            :placeholder="task.title"
            v-model="task.title"
            v-bind:disabled="!editable"
            v-bind:class="{ completed: task.completed }"
          />
        </form>
      </div>
      <div class="col-">
        <div>
          <button
            type="button"
            class="btn btn-success"
            @click="emitCompleted"
            v-if="!this.task.completed"
          >
            <font-awesome-icon icon="check" />
          </button>
          <button
            type="button"
            class="btn btn-primary"
            @click="emitCompleted"
            v-if="this.task.completed"
          >
            <font-awesome-icon icon="check" />
          </button>
        </div>
        <div>
          <button
            type="button"
            class="btn btn-warning"
            @click="enableEdit"
            v-if="!editable"
            v-bind:disabled="task.completed"
          >
            <font-awesome-icon icon="edit" />
          </button>
          <button
            type="button"
            class="btn btn-warning"
            @click="emitEdit"
            v-if="editable"
          >
            <font-awesome-icon icon="plus" />
          </button>
        </div>
        <div>
          <button type="button" class="btn btn-danger" @click="emitDelete">
            <font-awesome-icon icon="trash" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  data() {
    return {
      editable: false
    };
  },
  props: ["task"],
  /*mounted() {
    console.log(this.task.title);
  },*/
  methods: {
    emitDelete() {
      this.$emit("deleteEmitted", this.task);
    },

    enableEdit() {
      this.editable = true;
    },

    emitEdit() {
      this.editable = false;
      this.$emit("editEmitted", this.task);
    },

    emitCompleted() {
      if (this.task.completed === false) this.task.completed = true;
      else this.task.completed = false;
      this.$emit("editEmitted", this.task);
    }
  }
};
</script>

<style lang="sass">
.task
    text-align: center

.col-
    display: grid
    grid-template-columns: 1fr 1fr 1fr
    column-gap: 2px

.btn-warning, .btn-warning:hover, .btn-warning:focus, .btn-warning:disabled
    color: white

button
    width: 44px

.completed
    background-color: #bdecb6 !important
</style>
