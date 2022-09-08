<script setup>
import TimelineItem from './components/TimelineItem.vue'
import data from "./data.json";
</script>


<template>
  <main>
    <h1 class="title">ES Timeline</h1>
    <div class="timeline">
          <div  class="timeline__item" v-for="row in sortedItems" :key="row._id">
            <TimelineItem :data="row" />
          </div>
    </div>
  </main>
</template>

<script>
  export default {
   computed: {
    sortedItems: function() {
      return this.data.sort((a, b) => new Date(a.registered) - new Date(b.registered))
    }
  }
 }
 </script>

<style lang="scss">
  .timeline {
    position: relative;

    &:before {
      content: "";
      position: absolute;
      left: 50%;
      top: 0;
      height: 100%;
      width: 3px;
      background-color: var(--color-primary);
    }

    &__item {
      width: 50%;
      padding: 0 6em;

      .name {
        font-size: 2rem;
        font-weight: 600;
        margin: 0.5em 0;
      }

      .date {
        margin: 0.5em 0;
      }

      .tags {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        margin: 1em 0;

        &__item {
          font-size: 0.8em;
          padding: 0.25em 0.5em;
          margin: 0.5em;
          border-radius: 5px;
          background-color: var(--color-active)
        }
      }


      &:before {
        content: "";
      }

      &:after {
        content: "";
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto;
        right: -15px;
        height: 30px;
        width: 30px;
        background-color: var(--color-active);
        border-radius: 50px;
      }

      &:nth-of-type(even) {
        margin-left: 50%;

        &:after {
          right: auto;
          left: -15px;
        }
      }
    }
  }
</style>

