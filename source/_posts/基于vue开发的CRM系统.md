---
title: vue后台管理系统
date: 2021-10-29 14:16:48
tags:
---

##### 1. 功能模块
（1）客户管理
    - 仪表盘
    - 待办事项
    - 线索
    - 客户
    - 联系人
    - 商机
    - 合同
    - 回款
    - 发票
    - 产品
    - 市场活动
（2）人力资源
（3）日志
（4）项目管理
（5）任务审批

##### 2. 技术栈
vue@2.x
vue-cli@3.x
vue-router
vuex
axios
element-ui

##### 3. 搭建开发环境
(1) 安装node
(2) 安装vue-cli

```
npm install vue-cli -g
```

##### 4. 项目初始化
```
vue create crm
```

##### 5. github管理代码
（1）github上创建远程代码仓库


##### 6. 项目规划
|- api
|- assets
|- components
    |- CreateView.vue   // 新建页面通用组件
|- directives
|- filters
|- router
|- store
|- styles
|- utils
|- views
    |- CustomerManagement
        |- components
            |- CrmListHead.vue // 客户管理通用页头
        |- customer
            |- CustomerIndex.vue
|- App.vue
|- main.js
|- permission.js

##### 6. axios封装

```
import axios from 'axios'

const service = axios.create({
    baseURL: process.env.BASE_API,
    timeout: 15000
})

service.interceptors.request.use(config => {

})

service.interceptors.response.use(response => {

})

export default service
```

##### 7. 请求API

api/user.js

```
import request from '@/utils/request'

export default login (username, password) {
    return request({
        url: '/login',
        data: {
            username,
            password
        }
    })
}
```

##### 8. 公共模块封装
（1）新建页面组件

```
<template>
    <transition name="opacity-fade">
        <div 
            class="c-view"
            :style="{'background-color': backgroundColor, 'padding': padding}"
        >
            <el-card
                v-loading="loading"
                :style="{'width': width}"
            >
                <slot name="header" />
                <slot />
            </el-card>
        </div>
    </transition>
</template>
<script>
export default {
    name: 'CreateView',
    props: {
        borderStyle: {
            type: Object,
            default: () => {
                return {}
            }
        },
        loading: {
            type: Boolean,
            default: false
        },
        width: {
            type: String,
            default: '700px'
        },
        backgroundColor: {
            type: String,
            default: '#F5F6F9' // rgba(0, 0, 0, 0.6) 黑色半透明
        },
        /** 展示内容的上下padding **/
        padding: {
            type: String,
            default: '40px'
        }
    },
    data () {
        return {
            
        }
    }
}
</script>
<style lang="scss" scoped>
.opacity-fade-enter,
.opacity-fade-leave-active{
    transition: all 0.2s;
}
.opacity-fade-enter,
.opacity-fade-leave-to{
    opacity: 0;
}
</style>
```

##### 7. 状态管理
- store/index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
import getters from './getters'
import customer from './modules/customer'

Vue.use(Vuex)

const store = new Vuex.Store({
    modules: {
        app,
        customer
    },
    getters
})

export default store
```

- store/getters.js

```
const getters = {
    crm: state => state.user.crm
}

export default getters
```

- store/modules/user.js

```
import { login, logout } from '@/api/login'
const app = {
    state: {
        crm: {},    // 客户管理
    },
    mutations: {
        SET_CRM: (state, crm) => {
            state.crm = crm
        }
    },
    actions: {
        Login({commit}, userInfo){
            return new Promise((resolve, reject) => {
                login(username, userInfo.password).then(data => {
                    commit('SET_CRM', data.auth.crm)
                }).catch(error => {
                    reject(error)
                })
            })
        }
    }
}
export default app
```

##### 6. 客户模块
（1）

（2）分析页面，筛选通用部分，封装成公共组件
- 页头部分公用组件封装
CrmListHead
```
<template>
    <div class="container">
        <div>{{title}}</div>
        <el-input 
            placeholder="placeholder"
            @input="inputChange"
            v-model="inputContent">
            <el-button 
                icon="el-icon-search"
                @click.native="searchInput" />
        </el-input>  
        <div class="right-container">
            <el-button 
                v-if="cansave"
                type="primary"
                @click="createClick"
            >{{mainTitle}}</el-button>
            <el-dropdowm
                v-if="moreTypes.length > 0"
                trigger="click"
                @command="handleTypeDrop"
            >
                <el-dropdown-menu slot="dropdown">
                    <el-dropwdown-item
                        v-for="(item, index) in moreTypes"
                        :key="index"
                    >
                        {{iitem.name}}
                    </el-dropdowm>
                </el-dropdown-menu>
            <el-dropdown>
        </div>
        <crm-create-view 
            v-if="isCreate"
            :crmType=""
        />
    </div>
</template>

<script>
import { mapGetters } from 'vuex'
import CrmCreateView from '@/components/CrmCreateView'
export default {
    name: 'CrmListHead',
    components: {
        CrmCreateView
    },
    data () {
        return {
            inputContent: '',
            moreTypes: []
        }
    },
    props: {
        // 页头主标题
        title: {
            type: String,
            default: '
        },
        placeholder: {
            type: String,
            default: '请输入内容'
        },
        // 页头按钮文字
        mainTitle: {
            type: String,
            default: ''
        },
        crmType: {
            type: String,
            default: ''
        },
        isSeas: {
            type: Boolean,
            default: false
        }
    },
    computed: {
        ...mapGetters(['crm']),
        canSave () {

        }
    },
    mounted () {
        // 线索和客户判断更多操作
        if (!this.isSeas) {
            if (this.crm[this.crmType].excelimport) {
                this.moreTypes.push({type: 'enter', name: '导入'})
            }
            if (this.crm[this.crmType].excelexport) {
                this.moreTypes.push({type: 'out', name: '导出'})
            }
        } else {
             // 客户池的导出关键字不同
            if (this.crm.pool.excelexport) {
                this.moreTypes.push({ type: 'out', name: '导出' })
            }
        }
    },
    methods: {
        // 下拉菜单点击
        handleTypeDrop(command, param = {}) {
            if (command === 'out') {

            } else if (command === 'enter') {

            }
        }
        inputChange() {
            this.$emit('update:search', this.inputContent)
        },
        searchInput () {
            this.$emit('on-search', this.inputContent)
        },
        // 新建按钮
        createClick () {

        }
    }
}
</script>
```

（2）mixins

mixin/table.js

```
import {
    crmCustomerIndex
} from '@/api/customerManagment/customer'
export default {
    components: {
        CrmListHead,
    },
    data () {
        return {
            loading: false, // 是否加载中
            list: [],   // 表格数据
            search: ''  // 搜索内容
            fieldList: [],  // 表格字段
            currentPage: 1, // 当前页面
            total: 0,   // 总页数
            pageSize: [15, 30, 60, 100],    
            selectList: [], // 选中的数据
        }
    },
    computed: {
        ...mapGetters(['crm'])
    },
    mounted () {
        // 控制table的高度
        window.resize = () => {
            this.updateTableHeight()
        }
    },
    methods: {
        // 获取数据
        getList () {
            this.loading = true
            var crmIndexRequest = this.getIndexRequest()
            // API请求参数
            var params = {
                page: this.currentPage,
                limit: this.pageSize,
                search: this.search,
                type: this.isSeas ? crmTypeModel.pool : crmTypeModel[this.crmType]
            }
            // 执行请求
            crmIndexRequest(params).then(res => {
                if () {

                } else {
                    this.list = res.data.list
                }
                this.total = res.data.totalRow
                this.loading = false
            }).catch(() =>  {
                this.loading = false
            })
        },
        // 判断当前页面要执行的API请求
        getIndexRequest () {
            if (this.crmType === 'leads') {
                return crmLeadsIndex
            } else if (this.crmType === 'customer') {
                if (this.isSeas) {
                    return crmCustomerPool
                } else {
                    return crmCustomerIndex
                }
            } else if (this.crmType === 'contacts') {
                return crmContactsIndex
            } else if (this.crmType === 'business') {
                return crmBusinessIndex
            } else if (this.crmType === 'product') {
                return crmProductIndex
            }
        },
        // 搜索
        crmSearch (value) {

        }
        // 获取表格字段
        getFieldList () {
            
        }
    }
}
```

（3）客户管理页面

CustomerIndex.vue

```
<template>
    <crm-list-head 
        ref="listHead"
        title="客户管理"
        :crm-type="crmType"
        placeholder="请输入客户名称/手机号"
        main-title="新建客户"
    />
    <div>
        <crm-table-head 

        />
        <el-table
            v-loading="loading"
            :data="list"
            style="width: 100%"
            border
            stripe
        >
            <el-table-column
                show-overflow-tooltip
                type="selection"
                align="center"
                width="55"
            />
            <!-- 遍历字段 -->
            <el-table-column
                v-for="(item, index) in fieldList"
                :key="item.id"
                :prop="item.prop"
                :label="item.label"
                sortable="custom"
                show-overflow-tooltip
            >
                <template
                    slot="header"
                    slot-scope="scope"
                >
                    <div class="table-head-name">{{scope.column.label}}</div>
                </template>
            <el-table-column/>
            <el-table-column
                fixed="right"
                width="36"
             >
                
             </el-table-column>
        </el-table>
        <!-- 分页 -->
        <div class="p-container">
            <el-pagition 
                class="p-bar"
                :current-page="currentPage"
                :page-sizes="pageSizes"
                :titla="total"
                layout="totla, sizes, next, prev, jumper"
                @current-change="handleCurrentChange"
            />
        </div>
    </div>
</template>
<script>
import { mapGetters } from 'vuex'
export default {
    name: 'CustomerIndex',
    components: {

    },
    computed: {
        ...mapGetters(['CRMconfig'])
    },
    minins: [],
    data () {
        return {
            crmType: 'customer'
        }
    },
    methods: {

    }
}
</script>
<style lang="scss" scoped>

</style>
```
