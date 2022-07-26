<template>
  <v-container>
    <v-card>
      <v-container>
        <div class="createForm">
          <v-form @submit.prevent="createTodo">
            <div class="textfields">
              <v-text-field label="Titel" v-model="title" />

              <template>
                <v-menu
                  ref="menu"
                  v-model="menu"
                  :close-on-content-click="false"
                  transition="scale-transition"
                  offset-y
                  min-width="290px"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-text-field
                      v-model="date"
                      label="Datum"
                      prepend-icon="mdi-calender"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    ref="picker"
                    locale="de"
                    :first-day-of-week="1"
                    v-model="date"
                    :min="new Date().toISOString().substr(0, 10)"
                    @change="save"
                  ></v-date-picker>
                </v-menu>
              </template>
            </div>
            <v-textarea v-model="desc" label="Beschreibung" outlined class="" />
            <v-chip @click="important = !important" :class="activeColor">
              wichtig
            </v-chip>

            <v-btn class="buttonCreateTodo" dark type="submit" color="green">
              create</v-btn
            >
          </v-form>
        </div>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "CreateTodo",
  data() {
    return {
      title: "",
      desc: "",
      isComplete: false,
      important: false,
      date: null,
      due: null,
      menu: false,
    };
  },
  watch: {
    menu(val) {
      val && setTimeout(() => (this.$refs.picker.activePicker = "YEAR"));
    },
  },
  methods: {
    save(date) {
      this.$refs.menu.save(date);
    },
    createTodo(event) {
      console.log(event.target.checked);
      axios({
        method: "post",
        url: `https://vue-todo-backend.azurewebsites.net/todos/`,
        data: this.$data,
      }).then((data) => {
        this.$emit("todo-updated", data.data);
        console.log("todo updated");
      });
    },
  },
  computed: {
    activeColor() {
      return this.important ? "active" : "notActive";
    },
  },
};
</script>

<style>
.active {
  background-color: rgba(255, 0, 0, 1) !important;
  color: white !important;
  float: left;
}

.notActive {
  color: rgba(0, 0, 0, 0.4) !important;
  float: left;
}

.buttonCreateTodo {
  left: 60%;
}
</style>
