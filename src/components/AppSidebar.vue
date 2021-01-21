<template>
  <form class="card card-w30" @submit.prevent="resetForm">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea v-model="content" id="value" rows="3"></textarea>
    </div>

    <button
      class="btn primary"
      @click="$emit('sendBlock', content, type)"
      type="submit"
      :disabled="watchTextarea"
    >Добавить</button>
  </form>
</template>

<script>

export default {
  props: {},
  emits: ['sendBlock'],
  data () {
    return {
      content: '',
      type: 'title'
    }
  },
  methods: {
    resetForm () {
      this.content = ''
      this.type = 'title'
    }
  },
  computed: {
    watchTextarea () {
      return this.content.length < 4
    }
  }
}
</script>

<style scoped>

</style>
