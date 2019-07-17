# iview-table-page

## Install
```
$ npm i --save iview-table-page
or
yarn add iview-table-page
```
## API
[API](./doc/api.md)
## Demos
[服务端分页以及自定义序号](./example/table1.vue)
[服务端分页并排序、过滤](./example/table2.vue)
[可编辑单元格](./example/table3.vue)
[可编辑行](./example/table4.vue)

## Quick Start
### 全局注册组件
Import modules and set up settings in `main.js`:

```js
import Vue from 'vue'
import iviewTablePage from 'iview-table-page'
Vue.use(iviewTablePage)
```
### 局部注册组件
```js
<template>
<div>
  <iviewTablePage
  border
  :columns="columns7"
  :data="data6"
  :total='total'
  >
  </iviewTablePage>
</div>
</template>

<script>
import iviewTablePage from 'iview-table-page'
export default {
  components: { iviewTablePage },
  data () {
    return {
      columns7: [
        {
          title: 'Name',
          key: 'name',
          render: (h, params) => {
            return h('div', [
              h('Icon', {
                props: {
                  type: 'person'
                }
              }),
              h('strong', params.row.name)
            ])
          }
        },
        {
          title: 'Age',
          key: 'age'
        },
        {
          title: 'Address',
          key: 'address'
        },
        {
          title: 'Action',
          key: 'action',
          width: 150,
          align: 'center',
          render: (h, params) => {
            return h('div', [
              h(
                'Button',
                {
                  props: {
                    type: 'primary',
                    size: 'small'
                  },
                  style: {
                    marginRight: '5px'
                  },
                  on: {
                    click: () => {
                      this.show(params.index)
                    }
                  }
                },
                'View'
              ),
              h(
                'Button',
                {
                  props: {
                    type: 'error',
                    size: 'small'
                  },
                  on: {
                    click: () => {
                      this.remove(params.index)
                    }
                  }
                },
                'Delete'
              )
            ])
          }
        }
      ],
      data6: [
        {
          name: 'John Brown',
          age: 18,
          address: 'New York No. 1 Lake Park'
        },
        {
          name: 'Jim Green',
          age: 24,
          address: 'London No. 1 Lake Park'
        },
        {
          name: 'Joe Black',
          age: 30,
          address: 'Sydney No. 1 Lake Park'
        },
        {
          name: 'Jon Snow',
          age: 26,
          address: 'Ottawa No. 2 Lake Park'
        }
      ],
      total: 4
    }
  }
}
</script>

```
## LICENSE
MIT