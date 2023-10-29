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
    <button @click="() => showList = !showList">
      Ver a lista!
    </button>
    <br>
    <input type="text" v-focus>
    <ul v-if="showList">
      <li
        v-for="(task, index) in tasks"
        :key="`${task}-${index}`"
      >
        {{ task.name }}
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
      ]
  })
}
</script>