# api说明
## table 属性

属性 | 说明 | 类型 | 默认值
---|--- | --- | ---
data | 显示的结构化数据，其中，字段 cellClassName 用于设置任意单元格的样式名称，因此数据不能使用该字段，详见示例特定样式。 | Array | []
columns | 表格列的配置描述，具体项见后文 | Array | []
stripe | 是否显示间隔斑马纹 | Boolean | false
border | 是否显示纵向边框 | Boolean | false
show-header | 是否显示表头 | Boolean | false
width | 表格宽度，单位 px | Number,String | 自动
height | 表格高度，单位 px，设置后，如果表格内容大于此值，会固定表头 | Number,String | -
max-height  | 表格最大高度，单位 px，设置后，如果表格内容大于此值，会固定表头 | Number,String | -
loading | 表格是否加载中 | Boolean	| false
disabled-hover | 禁用鼠标悬停时的高亮 | Boolean | false
highlight-row | 是否支持高亮选中的行，即单选 | Boolean | false
row-class-name | 行的 className 的回调方法，传入参数：row：当前行数据,index：当前行的索引 | Function | -
size | 表格尺寸，可选值为 large、small、default 或者不填 | String | -
no-data-text | 数据为空时显示的提示内容 | String | 暂无数据
no-filtered-data-text | 筛选数据为空时显示的提示内容 | String | 暂无筛选结果
draggable | 是否开启拖拽调整行顺序，需配合 @on-drag-drop 事件使用 | Boolean | false
tooltip-theme | 列使用 tooltip 时，配置它的主题，可选值为 dark 或 light | String | dark
row-key | 是否强制使用内置的 row-key，开启后可能会影响性能 | Boolean | false

## table事件
事件名 | 说明 | 返回值
---|---|--- 
on-current-change | 开启 highlight-row 后有效，当表格的当前行发生变化的时候会触发 | currentRow：当前高亮行的数据,oldCurrentRow：上一次高亮的数据
on-select | 在多选模式下有效，选中某一项时触发 | selection：已选项数据,row：刚选择的项数据,即==接收的参数是（selection，row）==
on-select-cancel | 在多选模式下有效，取消选中某一项时触发 | selection：已选项数据，row：取消选择的项数据
on-select-all | 在多选模式下有效，点击全选时触发 | selection：已选项数据
on-select-all-cancel | 在多选模式下有效，点击取消全选时触发 | selection：已选项数据
on-selection-change | 在多选模式下有效，只要选中项发生变化时就会触发 | selection：已选项数据
on-sort-change | 排序时有效，当点击排序时触发 | column：当前列数据，key：排序依据的指标，order：排序的顺序，值为 asc 或 desc
on-filter-change | 筛选时有效，筛选条件发生变化时触发 | 当前列数据
on-row-click | 单击某一行时触发 | 当前行的数据，index
on-row-dblclick | 双击某一行时触发 | 当前行的数据，index
on-expand | 展开或收起某一行时触发 | row：当前行的数据，status：当前的状态
on-drag-drop | 拖拽排序松开时触发，返回置换的两行数据索引 | index1, index2

## page 属性
属性|	说明	|类型|	默认值
---|---|--- |---
==current==	|当前页码，支持 .sync 修饰符|	Number	|1
total|	数据总数|	Number|	0
page-size|	每页条数|	Number|	10
page-size-opts|	每页条数切换的配置|	Array|	[10, 20, 30, 40]
placement|	条数切换弹窗的展开方向，可选值为 bottom 和 top	|String	|bottom
==page-shape-size==|	可选值为small（迷你版）或不填（默认）|	String	|-
simple|	简洁版|	Boolean|	false
show-total|	显示总数	|Boolean|false
show-elevator|	显示电梯，可以快速切换到某一页|	Boolean	|false
show-sizer|	显示分页，用来改变page-size	|Boolean|	false
==page-class-name==|	自定义| class 名称	|String|	-
styles|	自定义 style 样式	|Object|	-
transfer|	是否将弹层放置于 body 内，在 Tabs、带有 fixed 的 Table 列内使用时，建议添加此属性，它将不受父级样式影响，从而达到更好的效果|	Boolean	|false
prev-text|	替代图标显示的上一页文字|	String|	-
next-text|	替代图标显示的下一页文字|	String|-

## 新增属性
属性|	说明	|类型|	默认值
---|---|--- |---
==pagination-show==	|是否显示页面|	Boolean	| true
==pagination-position== | 页码位置 | String 可选值为 left、center 和 right| right