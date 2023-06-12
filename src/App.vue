<template>
  <div
      class="h-screen w-screen bg-gradient-to-tr from-gray-900 to-white flex flex-col items-center justify-center px-4 space-y-3">
   

    <!-- List box -->
    <div class="bg-black p-8 w-full max-w-xl rounded">
      <!-- Add task -->
      <form @submit.prevent="addTask()" class="flex">
        <input
            v-model="taskInput"
            type="text"
            class="block w-full border border-gray-300 focus:border-gray-400 focus:outline-none rounded-l-md px-4 py-1.5"
            placeholder="Add task to your list"/>
        <button
            type="submit"
            class="border border-gray-300 border-l-0 rounded-r-md px-6 py-1 bg-indigo-900 hover:bg-indigo-400 text-white">
          Add
        </button>
      </form>
      <!-- Add task end-->

      <!-- Tasks List -->
      <div class="mt-5 space-y-1">
        <!---single task-->
        <div v-for="(task,index) in tasks" :key="index" class="px-3 py-1.5 bg-indigo-50 hover:bg-indigo-100 rounded flex items-center group">
          <input v-model="task.isComplete" :value="true" type="checkbox" class="w-4 h-4 rounded text-indigo-500 cursor-pointer"/>
          <span class="text-gray-800 ml-3" :class="{'line-through' : task.isComplete}"> {{ task.value }} </span>
          <button @click="removeTask(index)" class="text-red-500 ml-auto group-hover:block hidden hover:text-red-600">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                 stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
            </svg>
          </button>
        </div>
        <!--single task end-->
        <div v-if="tasks.length == 0" class="text-white text-center mt-8">
          You have no tasks :)
        </div>
      </div>
      <!-- Tasks List end -->

      <!-- Clear all -->
      <div @click="clearAll()" class="mt-4">
        <button class="px-6 py-1.5 text-white bg-indigo-900 hover:bg-indigo-400 rounded text-sm">
          Clear all
        </button>
      </div>
      <!-- Clear all end -->

    </div>
    <!-- List box end -->
  </div>
</template>

<script>


export default {
  data(){
    return{
       tasks: [],
       taskInput : null,
    }
  },
  methods:{
    addTask(){
      this.tasks.push({
        value: this.taskInput,
        isComplete: false
      })
      this.taskInput= null
    },
    removeTask(index){
      this.tasks.splice(index, 1)
    },
    clearAll(){
      this.tasks=[]
    }
  }
}

</script>