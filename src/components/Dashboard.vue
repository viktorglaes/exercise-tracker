<template>
  <div class="dashboard">
    <div class="exercises" v-for="exercise in exercises" :key="exercise.id">
      <div class="exercise">
        <div class="exercise-type">{{ exercise.type }}</div>
        <div class="exercise-time">{{ exercise.time }}</div>
        <div class="exercise-date">{{ exercise.date }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import eventbus from "../event-bus.js";
export default {
  name: "Dashboard",
  data() {
    return {
      exercises: [],
    };
  },
  mounted() {
    eventbus.$on("SEND_ARRAY", (data) => {
      this.exercises.push(data);
    });
  },
};
</script>

<style lang="scss">
.dashboard {
  min-height: 300px;
  max-height: 300px;
  overflow: scroll;
  .exercises {
    .exercise {
      margin: 2rem;
      min-height: 4rem;
      max-width: 20rem;
      border-radius: 20rem;
      text-align: center;
      background-color: lightblue;

      .exercise-type {
        font-weight: bold;
      }
    }
  }
}
</style>
