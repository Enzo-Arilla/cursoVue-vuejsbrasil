<template>
  <h1>Conceitos 1 e 2: Single-file components e Data-binding</h1>
  <h3 :style="{ textDecoration: decoration }">Olá, {{name}}</h3>
  <input type="text" v-model="name">
  <br>

  <a :href="link">Link pro curso!</a>

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
           v-model="currentTask">
    <ul v-if="showList">
      <li
        v-for="(task, index) in tasks"
        @dblclick="complete(task)"
        :key="`${task}-${index}`"
        class="task-item"
        :class="{
          'line-through': task.isDone
          }"
      >
        {{ task.name }}
        <button
          @click="remove(task)"
        >&times;</button>
      </li>
    </ul>
    <p v-else>Lista de tarefas escondidas</p>
  </div>



</template>

<script>

const focus = {
    inserted: (el) => {
      el.focus()
  }
}

export default {
  directives: {
    focus
  },
  data: () => ({
      name: 'Enzo',
      link: 'https://treinamento.vuejsbrasil.org',
      decoration: 'underline',
      showList: false,
      tasks: [
        { name: 'Fazer o curso', isDone: false},
        { name: 'Assistir o vídeo', isDone: true}
      ],
      currentTask: ''
  }),
  methods: {
      handleShowHideList () {
          this.showList = !this.showList
          this.remove()
      },
      addTask () {
          this.tasks.push({
              name: this.currentTask,
              isDone: false
          })
          this.currentTask = ''
      },
      complete (task) {
          this.tasks = this.tasks.map(t => {
              if (t.name === task.name) {
                  return { ...t, isDone: t.isDone}
              }
              return { ...t }
          })
      },
      remove (task) {
        this.tasks = this.tasks.filter(t => t.name !== task.name)
      }
  }
}
</script>

<style scoped>
.line-through {
    text-decoration: line-through;
}
.task-item {
    cursor: pointer;
}
</style>