<template>
  <div id="app" class="parent-app">
    <div class="header">
      <div class="icon">
        <img src="./assets/github.png" />
      </div>
      <div class="username">
        <a href="https://github.com/viktorglaes">@viktorglaes</a>
      </div>
    </div>
    <section class="hero is-success margin-top">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Exercise Tracking
          </h1>
          <h2 class="subtitle">
            Easily track your exercises with style
          </h2>
        </div>
      </div>
    </section>
    <div class="exercises">
      <section>
        <Dashboard :items="items">
          <template v-slot:default="{ item }">
            <div class="item">
              <!-- <img :src="item.image" alt="#" /> -->
              <img :src="require(`@/assets/${item.image}`)" alt="#" />
              <h5>{{ item.type }}</h5>
              <p>{{ item.time }}</p>
            </div>
          </template>
        </Dashboard>
      </section>
    </div>
    <Tracker />
  </div>
</template>

<script>
import Vue from "vue";
import Dashboard from "./components/Dashboard.vue";
import Tracker from "./components/Tracker.vue";
import eventbus from "./event-bus.js";

export default Vue.extend({
  name: "App",
  components: {
    Dashboard,
    Tracker,
  },
  data() {
    return {
      items: [
        {
          type: "Football",
          image: "soccer.jpg",
          time: "Less than two hours",
          date: "2020:09:24",
          id: 3001,
        },
        {
          comment: "",
          date: "2020:09:24",
          id: 3000,
          image: "climbing.jpg",
          time: "Less than one hour",
          type: "Climbing",
        },
        {
          comment: "",
          date: "2020:09:20",
          id: 3002,
          image: "running.jpg",
          time: "Less than one hour",
          type: "Running",
        },
        {
          comment: "",
          date: "2020:09:21",
          id: 3003,
          image: "walking.jpeg",
          time: "More than three hours",
          type: "Walking",
        },
        {
          comment: "",
          date: "2020:09:02",
          id: 3004,
          image: "climbing.jpg",
          time: "More than three hours",
          type: "Climbing",
        },
        {
          type: "Football",
          image: "soccer.jpg",
          time: "Less than two hours",
          date: "2020:09:24",
          id: 3005,
        },
      ],
    };
  },

  methods: {},

  mounted() {
    eventbus.$on("SEND_ITEM", (data) => {
      switch (data.type) {
        case "Climbing":
          data.image = "climbing.jpg";
          break;
        case "Football":
          data.image = "soccer.jpg";
          break;
        case "Running":
          data.image = "running.jpg";
          break;
        case "Walking":
          data.image = "walking.jpeg";
          break;
      }
      console.log(data);
      this.items.push(data);
    });
  },
});
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>

<style scoped lang="scss">
#app {
  font-family: "Roboto", sans-serif;
  margin-left: auto;
  margin-right: auto;
}

.exercises {
  padding: 0px 24px 40px 24px;
  min-height: 180px;
}

.header {
  display: flex;
  margin-top: 5px;
  margin-bottom: 5px;
  .icon {
    margin-left: 5px;
    height: 40px;
    width: 40px;
  }
  .username {
    margin-left: 10px;
    color: black;
    font-style: italic;
    padding: 10px 0px;
    font-weight: bold;
  }
}

@media (min-width: 1200px) {
  /* #app {
    padding-left: 80px;
    padding-right: 80px;
  } */
}

h5 {
  font-size: 18px;
  font-weight: bold;
  line-height: 1.5;
  margin: 0 0 8px;
}

p {
  font-size: 17px;
  line-height: 1.5;
  font-weight: 400;
  margin: 0;

  word-break: break-word;
}

.item {
  padding: 16px 24px;
  border-radius: 3px;
  background: lightblue;
}

/* section {
  margin-top: 24px;
} */
</style>
