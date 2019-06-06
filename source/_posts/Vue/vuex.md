---
title: Vuex
categories: ['前端']
tags: ['Vuex'] 
---
## 1.mapState 获取state值
---
    定义方式
    import {mapState} from ‘vuex’
    使用方式
    对象
    ```
    computed: mapState({
        count: state=>state.count
    })
    ```
    数组
    ```
    computed: mapState([count])
    ```
## 2.getter 获取state的值（过滤）
---
    定义方式
    写在vuex里面
    ```
    getters: {
        state => {
            return state.todos.filter(todo => todo.done) 过滤数据
        }
    }
    ```
    方法有两个参数（state,getters）getters（可以认为是 store 的计算属性）state是状态值

    getter也可以返回一个函数 getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果。
    ```
    getTodoById: (state) => (id) => {
        return state.todos.find(todo => todo.id === id)
    }
    store.getters.getTodoById(2) 
    ```
    使用方式
    import { mapGetters } from 'vuex'

    数组     使用对象展开运算符将 getter 混入 computed 对象中
    ```
    computed: {
        ...mapGetters([
        'doneTodosCount',
        'anotherGetter'
        ])
    }
    ```
    对象 （对象的好处是getter 属性另取一个名字)
    把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
    ```
    mapGetters({
        doneCount: 'doneTodosCount'
    })
    ```
## 3.Mutation（更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。同步）
    定义
    // mutation-types.js
    export const SOME_MUTATION = 'SOME_MUTATION' 
    // store.js
    import Vuex from 'vuex'
    import { SOME_MUTATION } from './mutation-types'
    ```
    const store = new Vuex.Store({
        state: { ... },
        mutations: {
            // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
            [SOME_MUTATION] (state,params) {
            // mutate state
            }
        }
    })
    ```
    使用
    import { mapMutations } from 'vuex'

    export default {
    // ...
    ```
    methods: {
        数组
        ...mapMutations([
            'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`

            // `mapMutations` 也支持载荷：
            'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
            ]),
        对象
        ...mapMutations({
            add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
        })
    }
    ```
## 4.Action 类似于 mutation，不同在于：

    Action 提交的是 mutation，而不是直接变更状态。
    Action 可以包含任意异步操作。
    定义
    ```
    actions: {
        increment (context) {
            context.commit('increment')
        }
    }
    ```
    Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 context.commit 提交一个 mutation，或者通过 context.state 和 context.getters 来获取 state 和 getters。当我们在之后介绍到 Modules 时，你就知道 context 对象为什么不是 store 实例本身了。
    ```
    actions: {
        increment ({commit}) {
            commit('increment')
        }
    }
    ```
    使用
    // 以载荷形式分发
    ```
    store.dispatch('incrementAsync', {
        amount: 10
    })

    // 以对象形式分发
    store.dispatch({
        type: 'incrementAsync',
        amount: 10
    })
    actions: {
        checkout ({ commit, state }, products) {
            // 把当前购物车的物品备份起来
            const savedCartItems = [...state.cart.added]
            // 发出结账请求，然后乐观地清空购物车
            commit(types.CHECKOUT_REQUEST)
            // 购物 API 接受一个成功回调和一个失败回调
            shop.buyProducts(
            products,
            // 成功操作
            () => commit(types.CHECKOUT_SUCCESS),
            // 失败操作
            () => commit(types.CHECKOUT_FAILURE, savedCartItems)
            )
        }
    }
    ```
    使用
    ```
    import { mapActions } from 'vuex'

    export default {
    // ...
    methods: {
        ...mapActions([
            'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

            // `mapActions` 也支持载荷：
            'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
        ]),
        ...mapActions({
            add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
        })
    }
    ```
    定义
    actions结束后触发函数
    ```
    actions: {
        actionA ({ commit }) {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    commit('someMutation')
                    resolve()
                }, 1000)
            })
        }
    }
    ```
    使用
    ```
    store.dispatch('actionA').then(() => {
    // ...
    })
    ```
    在另外一个 action 中也可以：
    ```
    actions: {
    // ...
    actionB ({ dispatch, commit }) {
            return dispatch('actionA').then(() => {
                commit('someOtherMutation')
            })
        }
    }
    ```
    最后，如果我们利用 async / await，我们可以如下组合 action：

    // 假设 getData() 和 getOtherData() 返回的是 Promise
    ```
    actions: {
        async actionA ({ commit }) {
            commit('gotData', await getData())
        },
        async actionB ({ dispatch, commit }) {
            await dispatch('actionA') // 等待 actionA 完成
            commit('gotOtherData', await getOtherData())
        }
    }
    ```

## 5.模块
    ```
    const moduleA = {
        state: { ... },
        mutations: { ... },
        actions: { ... },
        getters: { ... }
    }

    const moduleB = {
        state: { ... },
        mutations: { ... },
        actions: { ... }
    }

    const store = new Vuex.Store({
    modules: {
        a: moduleA,
        b: moduleB
    }
    })

    store.state.a // -> moduleA 的状态
    store.state.b // -> moduleB 的状态
    ```








