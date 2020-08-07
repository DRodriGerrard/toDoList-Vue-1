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
      <div class="col- buttons">
        <div>
          <button
            type="button"
            @click="emitCompleted"
            v-bind:class="{
              'btn btn-primary': task.completed,
              'btn btn-success': !task.completed
            }"
          >
            <font-awesome-icon icon="check" />
          </button>
        </div>
        <div>
          <button
            type="button"
            class="btn btn-warning"
            @click="handlerEdit"
            v-bind:disabled="task.completed"
          >
            <font-awesome-icon icon="edit" v-if="!editable" />
            <font-awesome-icon icon="plus" v-if="editable" />
          </button>
        </div>
        <div>
          <button type="button" class="btn btn-danger" @click="handlerDelete">
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
    handlerDelete() {
      this.$emit("deleteEmitted", this.task);
    },

    emitCompleted() {
      if (this.task.completed === false) this.task.completed = true;
      else this.task.completed = false;
      this.$emit("editEmitted", this.task);
    },

    handlerEdit() {
      if (this.editable == false) this.editable = true;
      else {
        this.editable = false;
        this.$emit("editEmitted", this.task);
      }
    }
  }
};
</script>

<style lang="sass">
.task
    text-align: center

.buttons
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
