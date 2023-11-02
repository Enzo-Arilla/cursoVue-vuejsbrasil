<template>
  <h1>Conceitos 1 e 2: Single-file components e Data-binding</h1>
  <h3 :style="{ textDecoration: data.decoration }">Olá, {{data.name}}</h3>
  <input type="text" v-model="data.name">
  <br>

  <a :href="data.link">Link pro curso!</a>

  <br><br>

  <h1>Conceito 3: Diretivas</h1>
  <div>
    <h3>Minha lista de tarefas!</h3>
    <br>
    <button @click="handleShowHideList">
      Ver a lista!
    </button>
    <br>
    <input type="text" 
           @keyup.enter="addTask" 
           v-focus 
           v-model="state.currentTask">
    <ul v-if="state.showList">
      <li
        v-for="(task, index) in state.tasks"
        @dblclick="complete(task)"
        :key="`${task}-${index}`"
        class="task-item"
        :class="{
          'line-through': task.isDone
          }"
      >
        {{ task.taskName }}
        <button
          @click="remove(task)"
        >&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tarefas escondidas</p>
  </div>
</template>

<script>
import { reactive } from "vue";
const focus = {
    inserted: (el) => {
      el.focus()
  }
}

export default {
    directives: {
        focus
    },
    setup() {

      const data = reactive({
           name: 'Enzo',
           link: 'https://treinamento.vuejsbrasil.org',
           decoration: 'underline'
      })

      const state = reactive({
        currentTask: '',
        showList: false,
        tasks: [
          { taskName: 'Fazer o curso', isDone: false}
        ]
      })

      function handleShowHideList () {
          state.showList = !state.showList
      }

      function addTask () {
          state.tasks.push({
              taskName: state.currentTask,
              isDone: false
          })
          state.currentTask = ''
      }

      function complete (task) {
          state.tasks = state.tasks.map(t => {
              if (t.taskName === task.taskName) {
                  return { ...t, isDone: t.isDone}
              }
              return { ...t }
          })
      }

      function remove (task) {
        state.tasks = state.tasks.filter(t => t.taskName !== task.taskName)
      }

      return {
        data,
        state,
        handleShowHideList,
        addTask,
        complete,
        remove
      }

    }
}

/*
export default {
  directives: {
    focus
  },
  data: () => ({
      name: 'Enzo',
      link: 'https://treinamento.vuejsbrasil.org',
      decoration: 'underline'
  }),
  methods: {
      handleShowHideList () {
          this.showList = !this.showList
          this.remove()
      },
      addTask () {
          this.tasks.push({
              taskName: this.currentTask,
              isDone: false
          })
          this.currentTask = ''
      },
      complete (task) {
          this.tasks = this.tasks.map(t => {
              if (t.taskName === task.taskName) {
                  return { ...t, isDone: t.isDone}
              }
              return { ...t }
          })
      },
      remove (task) {
        this.tasks = this.tasks.filter(t => t.taskName !== task.taskName)
      }
  }
}
*/
</script>

<style scoped>
.line-through {
    text-decoration: line-through;
}
.task-item {
    cursor: pointer;
}
</style>