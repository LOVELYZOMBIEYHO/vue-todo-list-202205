<!-- command: vbase-css -->

<template>
  <div class="w-full">
    <section id="input-area" class="m-auto w-1/2 px-8">
      <h1 class="text-2xl text-center font-semibold">
        {{ taskCount }} {{ taskCount == 1 ? "Task" : "Tasks" }}
      </h1>
      <!-- save input as variable -->
      <!-- Add a form to make enter key on the keyboard is work to push data, and should be prevent default submit  -->
      <!-- v:on:submit.prevent  is equal to  @submit.prevent-->
      <form @submit.prevent>
        <input
          :placeholder="'Add Task # ' + (tasks.length + 1)"
          class="border-2 border-black rounded-md w-full px-2 text-center"
          type="text"
          v-model="newTask"
        />
        <!-- trigger action to add the task || v-on:click == @onclick  -->
        <button
          @click="addTaskHandler"
          class="border-2 border-black rounded-md"
        >
          Add Task
        </button>
      </form>

      <!-- Example -->
      <!-- <code>
        <pre>
         {{ tasks }}
        </pre>
        <pre>
         {{ newTaskObject }}
        </pre>
      </code> -->
    </section>
    <br />
    <h3 class="m-auto w-1/2 px-8">
      ###Toggle tasks to mark the tasks finished and click the trash button to
      delete the item
    </h3>
    <br />
    <TaskList
      v-show="tasks.length"
      @deleteEvent="deleteEventHandler"
      @toggleComplete="toggleCompleteHandler"
      :tasks="tasks"
    />

    <!-- Make as component TaskList.vue -->

    <!-- <li v-for="task in tasks" v-bind:key="task.id">{{ task.name }}</li> -->
    <!-- <section id="task-list" class="w-1/2 mx-12">
      <ul class="m-auto justify-center">
        <li v-for="(task, i) in tasks" v-bind:key="i">{{ task.name }}</li>
      </ul>
    </section> -->
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue";

export default {
  name: "App",
  // data (vdata)
  // watchers (vwatcher)
  // methods or functions (vmethod)
  // computed properties (vcomputed)
  // components (vcomponents)

  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },

  methods: {
    deleteEventHandler(i) {
      this.tasks.splice(i, 1);
    },

    toggleCompleteHandler(i) {
      if (this.tasks.length < 1) return;
      const currentTaskCompleteStatus = this.tasks[i].complete;
      console.log(currentTaskCompleteStatus);
      const newCompleteValue = !currentTaskCompleteStatus;
      this.tasks[i].complete = newCompleteValue;
      // console.log("It worked! - ", i, "was clicked");
    },

    addTaskHandler() {
      // !this.newTask is equal to    this.newTask == ""
      if (!this.newTask) {
        return;
      } else {
        this.tasks.push(this.newTaskObject);
        // after push the data, make v-model="newTask" be empty
        this.newTask = "";
      }
    },
  },

  computed: {
    taskCount() {
      return this.tasks.length;
    },
    newTaskObject() {
      const newTaskObject = {
        id: this.tasks.length + 1,
        name: this.newTask,
        complete: false,
      };

      return newTaskObject;
    },
  },

  components: {
    TaskList,
  },
};
</script>

<style></style>
