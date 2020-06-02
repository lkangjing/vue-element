<template>
  <div class="tableWrap">
    <el-button @click="exportExcel">导出</el-button>
    <el-table
      id="out-table"
      :data="tableData"
      border
      :summary-method="getSummaries"
      show-summary
      height="200"
      style="width: 100%; margin-top: 20px"
    >
      <el-table-column
        prop="id"
        label="ID"
        width="180"
      />
      <el-table-column
        prop="name"
        label="姓名"
      />
      <el-table-column
        prop="amount1"
        label="数值 1（元）"
      />
      <el-table-column
        prop="amount2"
        label="数值 2（元）"
      />
      <el-table-column
        prop="amount3"
        label="数值 3（元）"
      />
    </el-table>
    <div style="height:20px" />
    <!-- <el-table
      :data="tableData"
      border
      show-summary
      style="width: 100%"
    >
      <el-table-column
        prop="id"
        label="ID"
        width="180"
      />
      <el-table-column
        prop="name"
        label="姓名"
      />
      <el-table-column
        prop="amount1"
        sortable
        label="数值 1"
      />
      <el-table-column
        prop="amount2"
        sortable
        label="数值 2"
      />
      <el-table-column
        prop="amount3"
        sortable
        label="数值 3"
      />
    </el-table> -->

    <img src="zzu-security-file.oss-cn-beijing.aliyuncs.com/2019-12-04/2f2996036d784a5db667385b6dc6b0ce-22222.jpg" alt="">
  </div>

</template>

<script>
import FileSaver from 'file-saver'
import XLSX from 'xlsx'
export default {
  data() {
    return {
      text: '共计',
      tableData: [{
        id: '12987122',
        name: '王小虎',
        amount1: '234',
        amount2: '3.2',
        amount3: 10
      },
      {
        id: '12987123',
        name: '王小虎',
        amount1: '165',
        amount2: '4.43',
        amount3: 12
      }, {
        id: '12987124',
        name: '王小虎',
        amount1: '324',
        amount2: '1.9',
        amount3: 9
      }, {
        id: '12987125',
        name: '王小虎',
        amount1: '621',
        amount2: '2.2',
        amount3: 17
      }, {
        id: '12987126',
        name: '王小虎',
        amount1: '539',
        amount2: '4.1',
        amount3: 15
      }]
    }
  },
  methods: {
    exportExcel() {
      /* generate workbook object from table */
      var wb = XLSX.utils.table_to_book(document.querySelector('#out-table'))
      /* get binary string as output */
      var wbout = XLSX.write(wb, { bookType: 'xlsx', bookSST: true, type: 'array' })
      try {
        FileSaver.saveAs(new Blob([wbout], { type: 'application/octet-stream' }), 'sheetjs.xlsx')
      } catch (e) { if (typeof console !== 'undefined') console.log(e, wbout) }
      return wbout
    },
    getSummaries(param) {
      const { columns, data } = param
      const sums = []
      columns.forEach((column, index) => {
        if (index === 0) {
          sums[index] = '总价'
          return
        }
        const values = data.map(item => Number(item[column.property]))
        if (!values.every(value => isNaN(value))) {
          sums[index] = values.reduce((prev, curr) => {
            const value = Number(curr)
            if (!isNaN(value)) {
              return prev + curr
            } else {
              return prev
            }
          }, 0)
          sums[index] += ' 元'
        } else {
          sums[index] = 'N/A'
        }
      })

      return sums
    }
  }
}
</script>
<style lang="scss" scoped>
    .tableWrap{
        padding: 50px;
    }
</style>
