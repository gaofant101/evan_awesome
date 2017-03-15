## Vuex

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能。

这个状态自管理应用包含以下几个部分：

- state，驱动应用的数据源；
- view，以声明方式将state映射到视图；
- actions，响应在view上的用户输入导致的状态变化。

![单一数据流](https://vuex.vuejs.org/zh-cn/images/flow.png)

但是，当我们的应用遇到多个组件共享状态时，单向数据流的简洁性很容易被破坏：

- 多个视图依赖于同一状态。
- 来自不同视图的行为需要变更同一状态。

![多组建共享状态](https://vuex.vuejs.org/zh-cn/images/vuex.png)

### 定义Store

	import Vue from 'vue'
	import Vuex from 'vuex'
	import * as actions from './actions'
	import * as getters from './getters'
	import mutations from './mutations'
	
	Vue.use(Vuex)
	
	const state = {
	    status: 'null'
	}
	
	export default new Vuex.Store({
	    state,
	    actions,
	    getters,
	    mutations
	})

### 定义type

	export const CHANGE_STATUS = 'CHANGE_STATUS'
	
### 定义突变 mutation 

	import * as types from './mutation-types'

	export default {
	    [types. CHANGE_STATUS] (state, status) {
	        state.status = status
	    }
	}

### 定义action

	import * as types from './mutation-types'

	export const changeStatus = ({ commit }, status) => {
	    commit(types. CHANGE_STATUS, status)
	}
	
### 定义 getter

	export const getStatus = state => state. status


### 调用

	export default {
        name: 'el',
        props: [''],    // props 可以是数组或对象，用于接收来自父组件的数据
        data () {
            // Vue 实例的数据对象
            // Vue 将会递归将 data 的属性转换为 getter/setter，从而让 data 的属性能够响应数据变化
            // 对象必须是纯粹的对象(含有零个或多个的key/value对)
        }
        computed: {
            ...mapGetters({
                status: 'getStatus'
            })
        },
        methods: {
            ...mapActions(['changeStatus'])
        }
    }

[Vuex 是什么？](https://vuex.vuejs.org/zh-cn/intro.html)