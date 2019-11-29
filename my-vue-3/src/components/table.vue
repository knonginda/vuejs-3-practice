<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th v-for="(column, $index) in columns" :key="$index">
            <div v-if="column.key in sort" class="th-sort">
              {{column.title}}
              <button @click="doSort(column.key)" type="button" v-if="sort[column.key] === 'asc'">↑</button>
              <button @click="doSort(column.key)" type="button" v-if="sort[column.key] === 'desc'">↓</button>
              <button @click="doSort(column.key)" type="button" class="sort-inactive" v-if="sort[column.key] === true">-</button>
            </div>
            <div v-else>
              {{column.title}}
            </div>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, rowIndex) in rows" :key="rowIndex">
          <td v-for="(column, columnIndex) in columns" :key="columnIndex">
            <table-expand
              v-if="column.render"
              :row="row"
              :column="column"
              :index="rowIndex"
              :render="column.render">
              </table-expand>
            <template v-else>
              {{row[column.key]}}
            </template>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import TableExpand from './expand'
import { cloneDeep } from 'lodash'

export default {
  name: 'Table',
  components: {
    TableExpand
  },
  props: {
    sort: {
      type: Object,
      default: () => ({})
    },
    columns: {
      type: Array,
      default: () => []
    },
    rows: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
    }
  },
  methods: {
    doSort (column) {
      let copySort = cloneDeep(this.sort)
      if (copySort[column] === 'desc') {
        copySort[column] = 'asc'
      } else if (copySort[column] === 'asc') {
        copySort[column] = true
      } else {
        copySort[column] = 'desc'
      }
      this.$emit('update:sort', copySort)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.table {
  width: 400px;
  border-collapse: collapse;
  border: 1px solid #000;
}

.table td, .table th {
  border: 1px solid #000;
  padding: 5px 10px;
}

.th-sort {
  display: flex;
  justify-content: space-around;
}

.th-sort button {
  border: 0;
  background: transparent;
  cursor: pointer;
  color: #333;
}

.th-sort button.sort-inactive {
  color: #999;
}
</style>
