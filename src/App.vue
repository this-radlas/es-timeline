<script setup>
import TimelineItem from "./components/TimelineItem.vue";
import data from "./data.json";
</script>

<template>
  <main>
    <h1 class="title">ES Timeline</h1>
    <div class="timeline">
      <div class="timeline__item" v-for="row in sortedItems" :key="row._id">
        <TimelineItem :data="row" />
      </div>
    </div>
  </main>
</template>

<script>
export default {
  computed: {
    sortedItems: function () {
      return this.data.sort(
        (a, b) => new Date(a.registered) - new Date(b.registered)
      );
    },
  },
};
</script>

<style lang="scss">
$bp-sm: 768px;

main {
  max-width: 1280px;
  margin: auto;
}

.title {
  text-align: center;
  font-size: 3rem;
  padding: 2em 0
}

.timeline {
  position: relative;

  &:before {
    content: "";
    position: absolute;
    top: 0;
    left: calc(3em - 4px);
    height: 100%;
    width: 4px;
    background-color: var(--color-primary);
    border-radius: 50px;

    @media (min-width: $bp-sm) {
      left: calc(50% - 1px);
    }
  }

  &__item {
    padding: 0 2em 0 6em;
    margin-bottom: 3em;

    @media (min-width: $bp-sm) {
      width: 50%;
      padding-right: 6em;
      text-align: center;
      margin-bottom: 0;
    }

    .name {
      font-size: 2rem;
      font-weight: 600;
      margin: 0.5em 0;
    }

    .date {
      margin: 0.5em 0;
    }

    p {
      font-size: 15px;
    }

    .tags {
      margin: 1em 0;

      &__item {
        display: inline-block;
        font-size: 0.8em;
        padding: 0.25em 0.5em;
        margin: 0 0.5em 0.5em 0;
        border-radius: 5px;
        background-color: var(--color-active);
        text-align: center;
        font-size: 13px;
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
      right: auto;
      left: calc(3em - 18px);
      height: 32px;
      width: 32px;
      background-color: var(--color-active);
      border-radius: 50px;
      box-shadow: 0 0 0 4px #fff;

      @media (min-width: $bp-sm) {
        right: -17px;
        left: auto;
      }
    }

    @media (min-width: $bp-sm) {
      &:nth-of-type(even) {
        margin-left: 50%;

        &:after {
          right: auto;
          left: -15px;
        }
      }
    }
  }
}
</style>
