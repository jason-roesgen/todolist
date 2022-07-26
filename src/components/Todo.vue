<template>
  <div class="todo mx-5">
    <v-container>
      <v-row>
        <v-col cols="10" class="pa-0">
          <v-list-item two-line>
            <v-list-item-content>
              <v-list-item-title>
                <v-checkbox
                  type="checkbox"
                  class="mt-0"
                  v-model="status"
                  @change="myAction"
                  :label="title"
                >
                </v-checkbox>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <div class="desc pl-12">
            {{ beschreibung }}
          </div>
          <div class="date pl-12">
            {{ formattedDate }}
          </div>
          <v-chip class="ma-2" v-if="important === true"> wichtig </v-chip>
        </v-col>
        <v-col cols="2" class="d-flex align-center">
          <v-btn x-small class="my-2" color="error" @click="deleteTodo" fab>
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Todo",
  props: ["id", "title", "date", "beschreibung", "status", "important"],
  methods: {
    myAction(event) {
      console.log(event.target.checked);
      axios({
        method: "patch",
        url: `https://vue-todo-backend.azurewebsites.net/todos/${this.id}`,
        data: {
          isComplete: event.target.checked,
        },
      }).then(() => {
        console.log("todo updated");
      });
    },
    deleteTodo() {
      axios({
        method: "delete",
        url: `https://vue-todo-backend.azurewebsites.net/todos/${this.id}`,
      }).then((todo) => {
        console.log("todo:" + todo);
        this.$emit("todo-deleted");
      });
    },
  },
  computed: {
    formattedDate() {
      return new Date(this.date).toLocaleDateString();
    },
  },
};
</script>

<style>
.date {
  margin-top: 8px;
}

.desc {
  color: rgba(0, 0, 0, 0.6);
  margin-top: -8px;
}

.todo {
  margin: 5px auto;
  width: 100%;
  padding: 0;
  border-radius: 25px;
  box-shadow: 0 10px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19) !important;
}

.todo .v-input .v-messages {
  display: none;
}

.todo .v-chip {
  background-color: red !important;
  left: 10%;
}

.todo .v-chip .v-chip__content {
  color: white;
}

.todo .v-list-item {
  height: 32px;
  min-height: 48px;
}

.todo .v-input__slot {
  margin-bottom: 0 !important;
}

.todo .theme--light.v-label {
  color: black !important;
}

.todo .theme--light.v-application {
  color: rgba(0, 0, 0, 0.6) !important;
}
</style>

