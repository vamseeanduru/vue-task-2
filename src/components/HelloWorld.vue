<template>
  <div class="overflow-auto">
    <div>
      <h1>{{ msg }}</h1>
    </div>
    <b-col md="3">
      <b-form-input type="search" v-model="filter" placeholder="Search" />
    </b-col>
    <br />
    <div>
      <b-table
        stripped
        bordered
        hover
        :per-page="perPage"
        :current-page="currentPage"
        :items="planetsList"
        :fields="fields"
        :filter="filter"
      ></b-table>
    </div>
    <b-pagination
      v-model="currentPage"
      :total-rows="10"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      perPage: 5,
      currentPage: 1,
      fields: ["name", "climate", "terrain", "population"],
      planetsList: [],
      filter: "",
    };
  },
  created() {
    this.getPlanetsList();
  },
  methods: {
    async getPlanetsList() {
      let vm = this;
      vm.planetsList = [];
      await axios
        .get("https://swapi.dev/api/planets")
        .then((res) => {
          vm.planetsList = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
h1 {
  font-size: 50px;
}
</style>
