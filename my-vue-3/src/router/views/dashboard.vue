<template>
  <div>
    <Table
      :columns="colunms"
      :rows="rows"
      :sort.sync="sort"
      @update:sort="doSort"
    >
    </Table>
  </div>
</template>

<script>
import Table from '@/components/Table'
export default {
  name: 'Dashboard',
  components: {
    Table
  },
  data () {
    return {
      sort: {
        name: 'desc',
        age: 'asc'
      },
      colunms: [
        {
          title: 'ID',
          key: 'id'
        },
        {
          title: '名字',
          key: 'name'
        },
        {
          title: '年龄',
          key: 'age',
          render: (h, params) => {
            return h('button', `操作 ${params.row.age}`)
          }
        }
      ],
      rows: [
        {
          id: '011',
          name: 'Yuhi',
          age: '30'
        },
        {
          id: '022',
          name: 'Elf',
          age: '21'
        },
        {
          id: '033',
          name: 'Moan',
          age: '30'
        }
      ]
    }
  },
  methods: {
    doSort (r) {
      // console.log(r)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
