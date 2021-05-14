<template>
  <div>
    <table class="table table-dark">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col">Name</th>
          <th class="tCases" scope="col">Total cases</th>
          <th class="tDeaths" scope="col">Total deaths</th>
          <th scope="col">Total recovered</th>
          <th class="newCases" scope="col">New cases</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(country, index) in countries"
          :key="index"
          @click="details(country.code)"
          class="cp"
        >
          <th class="table-light" scope="row">{{ country.CountryCode }}</th>
          <td class="table-info">{{ country.Country }}</td>
          <td class="table-warning">{{ country.TotalConfirmed }}</td>
          <td class="table-danger">{{ country.TotalDeaths }}</td>
          <td>{{ country.TotalRecovered }}</td>
          <td class="table-success">{{ country.NewConfirmed }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "table",
  mounted() {
    axios
      .get("https://api.covid19api.com/summary")
      .then((res) => {
        console.log(Object.values(res.data.Countries));
        this.countries = Object.values(res.data.Countries);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  data: function () {
    return {
      countries: null,
    };
  },
  methods: {
    details() {
      this.$router.push({
        name: "Details",
      });
    },
  },
};
</script>
<style>
.cp {
  cursor: pointer;
}
.newCases {
  color: Green;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
.tDeaths{
  color:red;
}
.tCases{
  color:yellow;
  font-family:Calibri;
  font-size:20px;
}
</style>
