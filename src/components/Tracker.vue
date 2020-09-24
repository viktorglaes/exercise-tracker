<template>
  <div class="exercise-form">
    <form>
      <div class="columns">
        <div class="column">
          <b-field label="Exercise">
            <b-select
              placeholder="Select an exercise"
              expanded
              v-model="item.type"
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
              <b-select placeholder="Time" v-model="item.time">
                <option value="Less than one hour">Less than one hour</option>
                <option value="Less than two hours">Less than two hours</option>
                <option value="Less than three hours"
                  >Less than three hours</option
                >
                <option value="More than three hours"
                  >More than three hours</option
                >
              </b-select>
            </b-field>
          </div>
        </div>
      </div>

      <b-field label="Comment">
        <b-input
          maxlength="1000"
          type="textarea"
          v-model="item.comment"
        ></b-input>
      </b-field>
      <div class="level-right">
        <b-button type="is-info" v-on:click="saveExercise">Save</b-button>
      </div>
    </form>
  </div>
</template>

<script>
import eventbus from "../event-bus";

export default {
  name: "Tracker",
  data() {
    return {
      item: {
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
      if (!this.item.type) {
        return;
      }
      this.item.date = this.addDate();
      eventbus.$emit("SEND_ITEM", this.item);
      this.item.id++;
      this.emptyForm(this.item.id);
    },
    emptyForm(id) {
      this.item = {
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
.exercise-form {
  height: 25rem;
  border-top: solid 1px gray;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  form {
    margin: 2rem;
  }
}
</style>
