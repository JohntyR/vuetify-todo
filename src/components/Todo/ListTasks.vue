<template>
  <v-list class="py-0" flat>
    <draggable
      v-model="tasks"
      handles=".handle"
    >
      <task
        v-for="task in tasks"
        :key="task.id"
        :task="task"
      />
    </draggable>
  </v-list>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  components: {
    task: require("@/components/Todo/Task.vue").default,
    draggable
  },
  computed: {
    tasks: {
      get() {
        return this.$store.getters.tasksFiltered;
      },
      set(value) {
        this.$store.dispatch('setTasks', value);
      },
    },
  },
};
</script>
