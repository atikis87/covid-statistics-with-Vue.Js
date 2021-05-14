<template>
  <div>
     <table class="table">
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Total cases</th>
      <th scope="col">Total deaths</th>
      <th scope="col">Total recovered</th>
      <th scope="col">New cases</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(country, index) in countries" :key="index" @click="details(country.code)" class="cp">
      <th scope="row">{{country.CountryCode}}</th>
      <td>{{country.Country}}</td>
      <td>{{country.TotalConfirmed}}</td>
      <td>{{country.TotalDeaths}}</td>
      <td>{{country.TotalRecovered}}</td>
      <td>{{country.NewConfirmed}}</td>
    </tr>
  </tbody>
</table> 
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name:"Table",
    mounted()
    {
        axios.get('https://api.covid19api.com/summary').then(res =>{
            console.log(Object.values(res.data.Countries));
            this.countries = Object.values(res.data.Countries);
        }).catch(err => {
            console.log(err);
        })
    },
    data: function()
    {
        return{
            countries: null
        }
    },
    methods:
    {
        details()
        {
            this.$router.push({
                name: "Details"
            })
        }
    }

};
</script>
<style>
.cp{
    cursor:pointer;
}
</style>