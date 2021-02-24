<template>
  <div>
    <h2 class="text-center">Catura tus Ideas</h2>
    <div class="card card-body bg-light">
      <h4 class="text-start">¿En qué estás pensando?</h4>
      <form v-on:submit.prevent="createIdea">
        <div class="input-group sm-3">
          <input v-model="newIdea" type="text" class="form-control" />
          <button
            type="submit"
            class="btn btn-outline-secondary"
            id="button-addon2"
          >
            Agregar
          </button>
        </div>
      </form>
      <hr />
      <ul class="list-unstyled">
        <li v-for="(idea, index) in ideas" :key="index">
          <p class="fs-6 text-start">
            <small class="text-muted">
              <em> {{ since(idea.created_at) }} </em>
            </small>
            {{ idea.description }}
          </p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import toastr from "toastr";
import moment from "moment";

moment.locale("es");

export default {
  mounted() {
    console.log("Component mounted.");
  },
  data() {
    return {
      ideas: [],
      newIdea: "",
    };
  },
  created: function () {
    this.getIdeas();
  },
  methods: {
    since: function (date) {
      return moment(date).fromNow();
    },
    getIdeas: function () {
      var urlIdeas = "mis-ideas";
      axios.get(urlIdeas).then((response) => {
        this.ideas = response.data;
      });
    },
    createIdea: function () {
      var url = "guardar-idea";
      axios
        .post(url, {
          description: this.newIdea,
        })
        .then((response) => {
          this.getIdeas();
          this.newIdea = "";
          toastr.success("Nueva idea registrada");
        })
        .catch((error) => {
          toastr.error("Error");
        });
    },
  },
};
</script>
