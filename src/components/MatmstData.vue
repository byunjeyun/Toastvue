<template>
  <div class="hello">
    <!-- <div class="search">
      <label>Part No: </label>
      <input v-model="searchText" @input="onSearchTextChange" />
    </div> -->
    <div class="grid-wrapper">
    <GridWrapper v-if="data.length" :data="data" :columns="columns" :rowHeaders="rowHeaders" :columnOptions="columnOptions"></GridWrapper>
    </div>
  </div>
</template>

<style>
.grid-wrapper {
  display: flex;
  width: fit-content;
  margin: auto;
}
</style>
<script>
import axios from 'axios';
import GridWrapper from './GridWrapper.vue';

export default {
  name: 'HelloWorld',
  components: {
    GridWrapper
  },
  data() {
  return {
    api: {
      readData: { url: 'http://localhost:8085/matmst', method: 'GET' }
    },
    data: [],
    columns: [
      {
        header: 'Part No',
        name: 'partno'
      },
      {
        header: 'Part Name',
        name: 'partnm'
      },
      {
        header: 'Material Group',
        name: 'mtgrp'
      },
      {
        header: 'Status',
        name: 'mtsts'
      },
      {
        header: 'GR Gate',
        name: 'roundval'
      },
      {
        header: 'Common Flag',
        name: 'configfg'
      },
      {
        header: 'Repack Qty ',
        name: 'dungfg'
      },
      {
        header: 'FC',
        name: 'updtdt'
      },
      {
        header: 'Auto.Repack',
        name: 'splarea'
      },
      {
        header: 'Feeding Unit ',
        name: 'glvarea'
      },
      {
        header: 'Loc.No',
        name: 'roundval'
      },
      {
        header: 'W/Station',
        name: 'roundval'
      },
      {
        header: 'Vendor',
        name: 'roundval'
      }
    ],
    rowHeaders: ['rowNum'],
    columnOptions: {
      minWidth: 150,
      resizable: true
    }
    
  };
},
  created() {
    this.getData();
  },
  methods: {
    getData() {
      axios
        .get('http://localhost:8085/matmst')
        .then((response) => {
          this.data = response.data.matmst_list;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  onSearchTextChange() {
      const grid = this.$refs.grid;
      const searchColumnName = 'partno';
      const searchText = this.searchText;
      grid.instance.setFilter(searchColumnName, (value) => {
        return value.includes(searchText);
      });
    }
  }
};
</script>