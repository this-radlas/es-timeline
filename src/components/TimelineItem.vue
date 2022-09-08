<template>
  <div class="date">{{ formatedDate }}</div>
    <div class="name">{{data.name.first + " " + data.name.last }}</div>
    <p>{{ data.about }}</p>
    <ul class="tags">
      <li v-for="tag in data.tags" class="tags__item">{{ tag }}</li>
    </ul>
</template>

<script>
export default {
  props: {
    data: Object,
  },
  computed: {
    formatedDate() {
        const date = new Date(this.data.registered);
        return `${date.getDate()}. ${date.getMonth() + 1}. ${date.getFullYear()}`;
    }
}
}
</script>

