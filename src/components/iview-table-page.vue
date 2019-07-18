<template>
<div>
     <Table
     :columns="columns"
     :data="data"
     :stripe='stripe'
     :border='border'
     :show-header='showHeader'
     :width='width'
     :height='height'
     :max-height='maxHeight'
     :loading='loading'
     :disabled-hover='disabledHover'
     :row-class-name='rowClassName'
     :size='size'
     :no-data-tex='noDataText'
     :no-filtered-data-text='noFilteredDataText'
     :draggable='draggable'
     :tooltip-theme='tooltipTheme'
     :row-key='rowKey'
     :highlight-row='highlightRow'

     @on-current-change='onCurrentChange'
     @on-select='onSelect'
     @on-select-cancel='onSelectCancel'
     @on-select-all='onSelectAll'
     @on-select-all-cancel='onSelectAllCancel'
     @on-selection-change='onSelectionChange'
     @on-sort-change='onSortChange'
     @on-filter-change='onFilterChange'
     @on-row-click='onRowClick'
     @on-row-dblclick='onRowDblclick'
     @on-expand='onExpand'
     @on-drag-drop='onDragDrop'>
      <template slot="header">
          <slot name='header'></slot>
      </template>
      <template slot="footer">
          <slot name='footer'></slot>
      </template>
      <template slot="loading">
          <slot name='loading'></slot>
      </template>
     </Table>
    <div :style="pageStyle" v-if="paginationShow">
        <Page
            :total="total"
            :current="current"
            :page-size='pageSize'
            :page-size-opts='pageSizeOpts'
            :placement='placement'
            :size='pageShapeSize'
            :simple='simple'
            :show-total='showTotal'
            :show-elevator='showElevator'
            :show-sizer='showSizer'
            :class-name='pageClassName'
            :styles='styles'
            :transfer='transfer'
            :prev-text='prevText'
            :next-text='nextText'

            @on-change='onChange'
            @on-page-size-change='onPageSizeChange'>
            <slot/>
            </Page>
    </div>
</div>
</template>

<script>
export default {
  name: 'iviewTablePage',
  props: {
    // 表格数据
    data: {
      type: Array,
      default: () => {
        return []
      }
    },
    // 表格列属性
    columns: {
      type: Array,
      default: () => {
        return []
      }
    },
    // 是否显示间隔斑马纹
    stripe: {
      type: Boolean,
      default: false
    },
    // 是否显示纵向边框
    border: {
      type: Boolean,
      default: false
    },
    // 是否显示表头
    showHeader: {
      type: Boolean,
      default: true
    },
    // 表格宽度，单位 px
    width: [String, Number],
    // 表格高度，单位 px，设置后，如果表格内容大于此值，会固定表头
    height: [String, Number],
    // 表格最大高度，单位 px，设置后，如果表格内容大于此值，会固定表头
    maxHeight: [String, Number],
    // 表格是否加载中
    loading: {
      type: Boolean,
      default: false
    },
    // 禁用鼠标悬停时的高亮
    disabledHover: {
      type: Boolean,
      default: false
    },
    // 是否支持高亮选中的行，即单选
    highlightRow: {
      type: Boolean,
      default: false
    },
    // 行的 className 的回调方法
    rowClassName: {
      type: Function,
      default: () => {
        return ''
      }
    },
    // 表格尺寸，可选值为 large、small、default 或者不填
    size: {
      type: String
    },
    // 数据为空时显示的提示内容
    noDataText: {
      type: String,
      default: '暂无数据'
    },
    // 筛选数据为空时显示的提示内容
    noFilteredDataText: {
      type: String,
      default: '暂无筛选结果'
    },
    // 是否开启拖拽调整行顺序，需配合 @on-drag-drop 事件使用
    draggable: {
      type: Boolean,
      default: false
    },
    // 列使用 tooltip 时，配置它的主题，可选值为 dark 或 light
    tooltipTheme: {
      type: String,
      default: 'dark'
    },
    // 是否强制使用内置的 row-key，开启后可能会影响性能
    rowKey: {
      type: Boolean,
      default: false
    },
    // 当前页码，支持 .sync 修饰符
    current: {
      type: Number,
      default: 1
    },
    // 数据总数
    total: {
      type: Number,
      default: 0
    },
    // 每页条数
    pageSize: {
      type: Number,
      default: 10
    },
    // 每页条数切换的配置
    pageSizeOpts: {
      type: Array,
      default: () => {
        return [10, 20, 30, 40]
      }
    },
    // 条数切换弹窗的展开方向，可选值为 bottom 和 top
    placement: {
      type: String,
      default: 'bottom'
    },
    // 可选值为small（迷你版）或不填（默认）
    pageShapeSize: {
      type: String
    },
    // 简洁版
    simple: {
      type: Boolean,
      default: false
    },
    // 显示总数
    showTotal: {
      type: Boolean,
      default: false
    },
    // 显示电梯，可以快速切换到某一页
    showElevator: {
      type: Boolean,
      default: false
    },
    // 显示分页，用来改变page-size
    showSizer: {
      type: Boolean,
      default: false
    },
    // 自定义 class 名称
    pageClassName: {
      type: String,
      default: ''
    },
    // 自定义 style 样式
    styles: {
      type: Object,
      default: () => {
        return {}
      }
    },
    // 是否将弹层放置于 body 内，在 Tabs、带有 fixed 的 Table 列内使用时，建议添加此属性，它将不受父级样式影响，从而达到更好的效果
    transfer: {
      type: Boolean,
      default: false
    },
    // 替代图标显示的上一页文字
    prevText: {
      type: String,
      default: ''
    },
    // 替代图标显示的下一页文字
    nextText: {
      type: String,
      default: ''
    },
    // 是否显示页码
    paginationShow: {
      type: Boolean,
      default: true
    },
    paginationPosition: {
      type: String,
      default: 'right'
    }
  },
  data () {
    return {
      pageStyle: {
        'text-align': this.paginationPosition,
        margin: '16px 0'
      }
    }
  },
  methods: {
    // 开启 highlight-row 后有效，当表格的当前行发生变化的时候会触发
    onCurrentChange (...arg) {
      this.$emit('on-current-change', ...arg)
    },
    // 在多选模式下有效，选中某一项时触发
    onSelect (...arg) {
      this.$emit('on-select', ...arg)
    },
    // 在多选模式下有效，取消选中某一项时触发
    onSelectCancel (...arg) {
      this.$emit('on-select-cancel', ...arg)
    },
    // 在多选模式下有效，点击全选时触发
    onSelectAll (...arg) {
      this.$emit('on-select-all', ...arg)
    },
    // 在多选模式下有效，点击取消全选时触发
    onSelectAllCancel (...arg) {
      this.$emit('on-select-all-cancel', ...arg)
    },
    // 在多选模式下有效，只要选中项发生变化时就会触发
    onSelectionChange (...arg) {
      this.$emit('on-selection-change', ...arg)
    },
    // 排序时有效，当点击排序时触发
    onSortChange (...arg) {
      this.$emit('on-sort-change', ...arg)
    },
    // 筛选时有效，筛选条件发生变化时触发
    onFilterChange (...arg) {
      this.$emit('on-filter-change', ...arg)
    },
    // 单击某一行时触发
    onRowClick (...arg) {
      this.$emit('on-row-click', ...arg)
    },
    // 双击某一行时触发
    onRowDblclick (...arg) {
      this.$emit('on-row-dblclick', ...arg)
    },
    // 展开或收起某一行时触发
    onExpand (...arg) {
      this.$emit('on-expand', ...arg)
    },
    // 拖拽排序松开时触发，返回置换的两行数据索引
    onDragDrop (...arg) {
      this.$emit('on-drag-drop', ...arg)
    },
    // 页码改变的回调，返回改变后的页码
    onChange (...arg) {
      this.$emit('on-change', ...arg)
    },
    // 切换每页条数时的回调，返回切换后的每页条数
    onPageSizeChange (...arg) {
      this.$emit('on-page-size-change', ...arg)
    },
    // 表格方法
    // 清除高亮项，仅在开启 highlight-row 时可用
    clearCurrentRow (...arg) {
      this.$children[0].clearCurrentRow(...arg)
    },
    // 表格方法
    // 全选或者取消全选
    selectAll (status) {
      this.$children[0].selectAll(status)
    },
    // 表格方法
    exportCsv (...arg) {
      this.$children[0].exportCsv(...arg)
    }
  },
  mounted () {
    let that = this
    // 获取跳转页码
    let dom = document.querySelector('.ivu-page-options-elevator input')
    if (dom) {
      dom.onchange = function () {
        let pageNo = parseInt(dom.value, 10)
        if (!Number.isNaN(pageNo) && pageNo > 0 && pageNo <= that.total) {
          that.current = pageNo
        }
      }
    }
  }
}
</script>
