<template>
  <div>
    <section id="task-list" class="mx-12 justify-center">
      <ul class="m-auto w-1/2 justify-center">
        <li class="flex" v-for="(task, i) in tasks" v-bind:key="i">
          <CustomButton
            :index="i"
            @btnClicked="deleteTaskHandler(i)"
            buttonType="trash"
          />
          <span
            @click="toggleCompeteHandler(i)"
            :class="['cursor-pointer ml-4', task.complete && 'line-through']"
          >
            {{ task.name }}
          </span>
          <span>
            {{ task.complete ? "DONE!" : "" }}
          </span>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
import CustomButton from "./uiElements/CustomButton.vue";

export default {
  name: "TaskList",
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    toggleCompeteHandler(i) {
      // Anything that's prefixed with the $ sign is automatically going to be binded to you Vue application so that you can access or use it globally
      this.$emit("toggleComplete", i);
      //   console.log("The task at index " + i + " was clicked");
    },
    deleteTaskHandler(i) {
      console.log("Delete", i);
      this.$emit("deleteEvent", i);
    },
  },

  components: {
    CustomButton,
  },
};
</script>

<style scoped></style>
