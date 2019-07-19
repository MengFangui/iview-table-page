<template>
<div>
    <h1>服务端分页并排序、过滤</h1>
    <iviewTablePage
    :columns="columns"
    :data="data"
    :total='total'
    :loading='loading'
    :current='current'
    :page-size='pageSize'
    show-sizer
    @on-change='handleChangeSize'
    @on-page-size-change='handlePageChangeSize'
    @on-sort-change="handleSortChange"
    @on-filter-change="handleFilterChange"
    >
    </iviewTablePage>
</div>
</template>
<script>
import iviewTablePage from 'iview-table-page'
import $ from './utils'
// 定义一个全局的变量，用来传递fiter过滤的值。
let filterType
export default {
  components: { iviewTablePage },
  data () {
    return {
      columns: [
        {
          title: '号码',
          key: 'number',
          // 服务端排序
          sortable: 'custom'
        },
        {
          title: '等级',
          key: 'status',
          render: (h, { row }) => {
            if (row.status === 1) {
              return h(
                'Tag',
                {
                  props: {
                    color: 'green'
                  }
                },
                '等级 1'
              )
            } else if (row.status === 2) {
              return h(
                'Tag',
                {
                  props: {
                    color: 'red'
                  }
                },
                '等级 2'
              )
            }
          },
          // 过滤
          filters: [
            {
              label: '级别 1',
              value: 1
            },
            {
              label: '级别 2',
              value: 2
            }
          ],
          filterMultiple: false,
          // 前端过滤
          // filterMethod(value, row) {
          //   if (value === 1) {
          //     return row.status === 1;
          //   } else if (value === 2) {
          //     return row.status === 2;
          //   }
          // }
          // 后端过滤
          filterRemote (value) {
            // 本行无效，this是本列数据，而不是vue实例
            this.filterType = value[0]
            filterType = value[0]
          }
        }
      ],
      data: [],
      loading: false,
      total: 0,
      current: 1,
      pageSize: 10,
      sortType: 'normal', // normal || asc || desc
      filterType: undefined // undefined, 1, 2
    }
  },
  methods: {
    handleSortChange ({ columns, key, order }) {
      this.sortType = order
      this.current = 1

      this.$nextTick().then(() => {
        this.getData()
      })
    },
    handleFilterChange () {
      this.current = 1
      // 重新赋值
      this.filterType = filterType
      this.$nextTick().then(() => {
        this.getData()
      })
    },
    getData () {
      if (this.loading) return

      this.loading = true

      $.ajax({
        method: 'get',
        url:
          '/data/list/' +
          this.current +
          '/' +
          this.sortType +
          '/' +
          this.filterType
      }).then(res => {
        setTimeout(() => {
          this.data = res.data.data.list
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
