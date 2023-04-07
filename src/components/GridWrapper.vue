<template>
    <div>
      <div ref="grid"></div>
      <slot></slot>
    </div>
  </template>
  
  <script>
  import Grid from 'tui-grid';
  import 'tui-grid/dist/tui-grid.css';
  
  export default {
    name: 'GridWrapper',
    props: {
      data: {
        type: Array,
        default: () => []
      },
      columns: {
        type: Array,
        default: () => []
      },
      rowHeaders: {
        type: [Array, Boolean],
        default: () => []
      },
      columnOptions: {
        type: Object,
        default: () => {}
      }
    },
    mounted() {
      this.grid = new Grid({
        el: this.$refs.grid,
        data: this.data, // 수정된 부분
        columns: this.columns,
        rowHeaders: this.rowHeaders,
        columnOptions: this.columnOptions
      });
    },
    beforeDestroy() {
      this.grid.destroy();
    }
  };
  </script>