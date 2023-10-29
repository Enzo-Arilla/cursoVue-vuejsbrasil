<template>
  <h1 :style="{ textDecoration: decoration }">Olá, {{name}}</h1>
  <input type="text" v-model="name">
  <br>

  <a :href="link">Link pro curso!</a>
</template>

<script>

export default {
  data: () => ({
      name: 'Enzo',
      link: 'https://treinamento.vuejsbrasil.org',
      decoration: 'underline'
  })
}
</script>