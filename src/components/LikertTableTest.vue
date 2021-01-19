<template>
  <div id="testTbl">
    <table-component
     :data="colorTable"
     sort-by="order"
     sort-order="asc"
     >
     <table-column show="value" label="Likert Names" :sortable="false" :filterable="false"></table-column>
     <table-column show="range" label="Ranges" :sortable="false" :filterable="false"></table-column>
     <table-column label="Color" :sortable="false" :filterable="false">
        <template slot-scope="row">
          <div :style="setBgColor(row.color)"></div>
        </template>
     </table-column>
    </table-component>
  </div>
</template>

<script>
import Vue from 'vue'
import { TableComponent, TableColumn } from 'vue-table-component'
import constant from "../utils/constants";
 
Vue.component('table-component', TableComponent)
Vue.component('table-column', TableColumn)

export default {
  name: "LikertTableTest",
  components: {
  },
   computed: {
    setBgColor() {
      return color => {
        return `background-color: ${color};height: 8px;`
      }
    }
  },
  data () {
    return {
      colorTable: [
     { value: 'To a very small extent', color: constant.BgColor.first.color , order: 1, range: '0% - 20%' },
     { value: 'To a small extent', color: constant.BgColor.second.color, order: 2, range: '20% - 40%' },
     { value: 'Somewhat', color: constant.BgColor.third.color, order: 3, range: '40% - 60%' },
     { value: 'To a great extent', color: constant.BgColor.fourth.color, order: 4, range: '60% - 80%' },
     { value: 'To a very great extent', color: constant.BgColor.fifth.color, order: 5, range: '80% - 100%' },
     ]
    }
  }
}
</script>