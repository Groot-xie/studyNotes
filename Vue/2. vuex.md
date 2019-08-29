## 第一步

```npm
npm i vuex
```

## 第二步

```js
// 在src目录下创建文件夹store   在store下创建文件index.js
// store/index.js

import Vuex from 'vuex'
import Vue from 'vue'
Vue.use(Vuex)

// 一个组件分为一个模块  方便管理
const home = {
  state: {
    // 预先给一个值
    a: []
  },
  mutations: {
    // 通过这个方法初始化数据a
    SET_HOME_DATA (store, arr) {
      store.a = arr
    }
  }
}

export default new Vuex.Store({
  modules: {
    home
  }
})
```

## 第三步

```js
// main.js
// 在main.js中导入store
import store from './vuex/index'
new Vue({
  el: '#app',
  store, // 写在这
  router,
  components: { App },
  template: '<App/>'
})
```

##  父组件获取数据初始化vuex中的数据

```js
// Home.vue
created () {
    const arr = [1, 2, 3]
    this.$store.commit('SET_HOME_DATA', arr)
  }
```

## 子组件获取数据使用

```js
// One.vue
created () {
    console.log('one', this.$store.state.home.a)
  }
```

## 之后项目大了可以拆分store  其实和模块是一样的

```js
// store/index.js

// 1.原本使用的是模块
import Vuex from 'vuex'
import Vue from 'vue'
Vue.use(Vuex)

const home = {
  state: {
    a: []
  },
  mutations: {
    SET_HOME_DATA (store, arr) {
      store.a = arr
    }
  }
}

export default new Vuex.Store({
  modules: {
    home
  }
})

// 2.将home组件的数据独立成为一个js文件，道理一样
// store/index.js
import Vuex from 'vuex'
import Vue from 'vue'
import home from './home'  // 和index同级创建home.js
Vue.use(Vuex)

export default new Vuex.Store({
  modules: {
    home
  }
})

// store/home.js
export default {
  state: {
    a: []
  },
  mutations: {
    SET_HOME_DATA (store, arr) {
      store.a = arr
    }
  }
}
```

