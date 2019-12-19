<template>
  <div>
    <el-row :gutter="15">
      <el-col :md="24" :sm="24">
        <el-card class="box-card m-b">
          <div slot="header">
            Multiple select
            
          </div>
         

          <el-table :data="tableData" ref="multipleTable" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="45"></el-table-column>
            <el-table-column sortable prop="date" label="Date" width="110"></el-table-column>
            <el-table-column prop="name" label="Name" width="110"></el-table-column>
            <el-table-column prop="address" label="Address"></el-table-column>
          </el-table>
          
           <el-button class="m-b" type="primary" size="mini" @click="toggleSelection(tableData)">Toggle selection</el-button>
          <el-button class="m-b" type="primary" size="mini" @click="toggleSelection()">Clear selection</el-button>

          <el-pagination layout="prev, pager, next, total, sizes, jumper" :total="tableData.total" 
            :page-size.sync="pageSize" :page-sizes="[2, 4, 6, 8, 10]" :current-page.sync="currentPage"
            @size-change="handleSizeChange" @current-change="handleCurrentChange"></el-pagination>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import { mapState, mapGetters, mapActions } from 'vuex'

  export default {
    data() {
      return {
        currentRow: null,
        multipleSelection: []
      }
    },
    computed: {
      ...mapState('table', ['tableData2', 'tableData3']),
      ...mapGetters('table', ['tableData'])
    },
    methods: {
      ...mapActions('table', ['getTableData', 'getTableData2', 'getTableData3']),
      tableRowClassName(row, index) {
        let color = ['text-primary', 'text-success', 'text-warning', 'text-danger']
        return color[index % color.length]
      },
      setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row)
      },
      handleCurrentChange(val) {
        this.currentRow = val
      },
      handleSelectionChange(val) {
        this.multipleSelection = val
      },
      toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row)
          })
        } else {
          this.$refs.multipleTable.clearSelection()
        }
      },
      filterTag(value, row) {
        return row.tag === value
      },
      getSummaries(param) {
        const { columns, data } = param
        const sums = []

        columns.forEach((column, index) => {
          if (index === 0) {
            sums[index] = 'Total Cost'
            return
          }

          const values = data.map(item => Number(item[column.property]))

          if (!values.every(value => isNaN(value))) {
            sums[index] = '$ ' + values.reduce((prev, curr) => {
              return prev + curr
            }, 0)
          } else {
            sums[index] = ''
          }
        })

        return sums
      },
      handleSizeChange: function(val) {
        this.getData(1, val)
      }
    },
    created() {
      this.getTableData2()
      this.getTableData3()
    }
  }
</script>