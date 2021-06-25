<template>
  <q-page class="bg-grey-3 column">
    <div class="q-pa-md bg-primary">
      <q-input
        dark
        filled
        v-model="newTask"
        placeholder="Add Task"
        dense
        @keydown.enter="addTask"
      >
        <template v-slot:append>
          <q-btn round dense flat icon="add" color="white" @click="addTask" />
        </template>
      </q-input>
    </div>

    <div v-if="tasks.length" class="q-gutter-sm">
      <q-list class="bg-white" separator bordered>
        <q-item
          v-for="(task, $index) in tasks"
          :key="$index"
          tag="label"
          v-ripple
          class="cursor-pointer"
          :class="{ 'done bg-deep-purple-1': task.done }"
        >
          <q-item-section avatar>
            <q-checkbox v-model="task.done" color="primary" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ task.title }}</q-item-label>
          </q-item-section>

          <q-item-section v-if="task.done" side>
            <q-btn
              @click.stop="confirmDelete($index)"
              :icon="'delete'"
              dense
              color="primary"
              flat
              round
            />
          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <div v-else class="absolute-center column items-center">
      <q-icon name="check" size="50px" color="grey-6"></q-icon>
      <p class="text-h6 text-weight-light text-grey-6 text-center">No Tasks</p>
    </div>

    <q-dialog v-model="showConfirmDialog" persistent>
      <q-card style="width: 500px; max-width: 80vw">
        <q-card-section>
          <div class="row items-center">
            <q-avatar icon="delete" color="primary" text-color="white" />
            <p class="q-ml-md q-mb-none text-h6 text-primary">Delete Task</p>
          </div>

          <p class="q-mt-lg q-py-sm q-ml-xs text-body1">
            Remove this task from Todo list?
          </p>
        </q-card-section>

        <q-card-actions align="right" class="bg-blue-grey-1 q-pa-md">
          <q-btn
            outline
            label="Cancel"
            color="primary"
            v-close-popup
            class="q-mr-sm"
          />
          <q-btn
            label="Yes, Delete Task"
            color="primary"
            @click="deleteTask"
            v-close-popup
          />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      deletedTasks: [],
      showConfirmDialog: false,
      taskToDelete: null,
      newTask: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          done: false,
        });

        this.newTask = "";
      }
    },
    confirmDelete(taskIndex) {
      this.showConfirmDialog = true;
      this.taskToDelete = taskIndex;
    },
    deleteTask() {
      const deletedTask = this.tasks.splice(this.taskToDelete, 1);
      this.deletedTasks.push(...deletedTask);

      this.$q.notify({
        message: "Task Deleted",
        color: "primary",
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.done {
  .q-item__label {
    color: #bbb;
    text-decoration: line-through;
  }
}

.no-tasks {
}
</style>