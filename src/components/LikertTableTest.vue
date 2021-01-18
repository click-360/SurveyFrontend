<template>
  <div id="testTbl">
    <table-component
     :data="colorTable"
     sort-by="order"
     sort-order="asc"
     >
     <table-column show="order" label="Order" data-type="numeric"></table-column>
     <table-column show="value" label="Likert Names"></table-column>
     <table-column show="range" label="Ranges" ></table-column>
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
     { value: 'Likert 1', color: constant.BgColor.first.color , order: 1, range: '0% to 20%' },
     { value: 'likert 2', color: constant.BgColor.second.color, order: 2, range: '20% to 40%' },
     { value: 'likert 3', color: constant.BgColor.third.color, order: 3, range: '40% to 60%' },
     { value: 'likert 4', color: constant.BgColor.fourth.color, order: 4, range: '60% to 80%' },
     { value: 'Likert 5', color: constant.BgColor.fifth.color, order: 5, range: '80% to 100%' },
     ]
    }
  }
}
</script>