<template>
  <div>
    <h2 class="text-center">Catura tus Ideas</h2>
    <div class="card card-body bg-light">
      <h4 class="text-start">¿En qué estás pensando?</h4>
      <form>
        <div class="input-group sm-3">
          <input type="text" class="form-control" />
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
              <em> {{ idea.created_at }} </em>
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

export default {
  mounted() {
    console.log("Component mounted.");
  },
  data() {
    return {
      ideas: [],
    };
  },
  created: function () {
    this.getIdeas();
  },
  methods: {
    getIdeas: function () {
      var urlIdeas = "mis-ideas";
      axios.get(urlIdeas).then((response) => {
        this.ideas = response.data;
      });
    },
  },
};
</script>
