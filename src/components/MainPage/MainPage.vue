<template>
  <div class="MainPage">
      <Header title="Covid Statistics"/>
      <Table />
  </div>
</template>

<script>

import Header from '../Header'
import Table from './Table'
export default {
  components:{Table, Header},

  props:{

  },
};
</script>
