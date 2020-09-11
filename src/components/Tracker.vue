<template>
  <div class="tracker">
    <form>
      <div class="columns">
        <div class="column">
          <b-field label="Exercise">
            <b-select
              placeholder="Select an exercise"
              expanded
              v-model="exercise.type"
            >
              <option value="Running">Running</option>
              <option value="Walking">Walking</option>
              <option value="Climbing">Climbing</option>
              <option value="Football">Football</option>
            </b-select>
          </b-field>
        </div>
        <div class="level-right">
          <div class="column">
            <b-field label="Time">
              <b-select placeholder="Time" v-model="exercise.time">
                <option value="less-one-hour"> Less than one hour</option>
                <option value="less-two-hours">Less than two hours</option>
                <option value="less-three-hours">Less than three hours</option>
                <option value="more-three-hours">More than three hours</option>
              </b-select>
            </b-field>
          </div>
        </div>
      </div>

      <b-field label="Comment">
        <b-input
          maxlength="1000"
          type="textarea"
          v-model="exercise.comment"
        ></b-input>
      </b-field>
      <div class="level-right">
        <b-button type="is-info" v-on:click="saveExercise">Save</b-button>
      </div>
    </form>
  </div>
</template>

<script>
import eventbus from "../event-bus.js";

export default {
  name: "Tracker",
  data() {
    return {
      exercise: {
        type: "",
        time: "",
        comment: "",
        id: 0,
        date: "",
      },
    };
  },
  methods: {
    saveExercise() {
      this.exercise.date = this.addDate();
      eventbus.$emit("SEND_ARRAY", this.exercise);
      this.exercise.id++;
      this.emptyForm(this.exercise.id);
    },
    emptyForm(id) {
      this.exercise = {
        type: "",
        time: "",
        comment: "",
        id: id,
      };
    },
    addDate() {
      let today = new Date();
      let date =
        today.getFullYear() +
        ":" +
        (today.getMonth() < 10 ? "0" : "") +
        (today.getMonth() + 1) +
        ":" +
        (today.getDate() < 10 ? "0" : "") +
        today.getDate();
      return date;
    },
  },
};
</script>

<style lang="scss">
.tracker {
  height: 25rem;
  background-color: #fcc9b9;
  form {
    margin: 2rem;
  }
}
</style>
