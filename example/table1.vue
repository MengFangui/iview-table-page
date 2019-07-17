<template>
    <iviewTablePage
    :columns="columns12"
    :data="data6"
    :total='total'
    :loading='loading'
    :current='current'
    :page-size='pageSize'
    show-sizer
    @on-change='handleChangeSize'
    @on-page-size-change='handlePageChangeSize'>
    </iviewTablePage>
</template>
<script>
import iviewTablePage from 'iview-table-page'
import $ from './utils'
export default {
  components: { iviewTablePage },
  data () {
    return {
      columns12: [
        {
          type: 'index',
          width: 60,
          align: 'center',
          indexMethod: row => {
            // 序号逻辑
            return row._index + 1 + this.pageSize * this.current - this.pageSize
          }
        },
        {
          title: '姓名',
          key: 'name'
        }
      ],
      data6: [],
      loading: false,
      total: 0,
      current: 1,
      pageSize: 10
    }
  },
  methods: {
    getData () {
      if (this.loading) return

      this.loading = true

      $.ajax({
        method: 'get',
        url: '/data/list/' + this.current + '/' + this.pageSize
      }).then(res => {
        setTimeout(() => {
          this.data6 = res.data.data.list
          this.total = res.data.data.total
          this.loading = false
        }, 1000)
      })
    },
    handleChangeSize (val) {
      this.current = val
      this.$nextTick(() => {
        this.getData()
      })
    },
    handlePageChangeSize (val) {
      this.pageSize = val
      this.$nextTick(() => {
        this.getData()
      })
    }
  },
  mounted () {
    this.getData()
  }
}
</script>
