# kfc-global-navigation
全局框架组件

## 功能
用于项目整体框架

## 维护者
youli

## 示例


## 测试组件

## router/navigation.js
```
import GlobalNavigation from '@/components/kfc-global-navigation'
import TestPage from '@/components/kfc-global-navigation/views/TestPage.vue'

export const navigation = {
  path: '/',
  name: 'goldwind',
  component: GlobalNavigation,
  children: [
    {
      path: 'user',
      name: 'user',
      component: TestPage,
      children: []
    },
    {
      path: 'user-detail',
      name: 'user-detail',
      component: TestPage,
      children: []
    },
    {
      path: 'role',
      name: 'role',
      component: TestPage,
      children: []
    },
    {
      path: 'group',
      name: 'group',
      component: TestPage,
      children: []
    },
    {
      path: 'group-detail',
      name: 'group-detail',
      component: TestPage,
      children: []
    },
    {
      path: 'model',
      name: 'model',
      component: TestPage,
      children: []
    },
    {
      path: 'model-detail',
      name: 'model-detail',
      component: TestPage,
      children: []
    },
    {
      path: 'bladed',
      name: 'bladed',
      component: TestPage,
      children: []
    },
    {
      path: 'tower',
      name: 'tower',
      component: TestPage,
      children: []
    },
    {
      path: 'tower-detail',
      name: 'tower-detail',
      component: TestPage,
      children: []
    }
  ]
}

```
router/ index.js 引入
```
import { navigation } from './navigation'

export default new Router({
  mode: 'history',
  base: process.env.BASE_URL,
  routes: [
    navigation
  ]
})

```
## store/module/menu.js
```
// 用户信息左侧菜单栏数据
const userList = [{
  title: '用户',
  icon: 'md-person',
  name: 'user',
  children: [
    {
      name: 'user',
      title: '用户列表'
    },
    {
      name: 'user-detail',
      title: '用户详情页面'
    }
  ]
}, {
  name: 'role',
  title: '角色',
  icon: 'ios-people'
}, {
  title: '分组',
  icon: 'ios-nuclear',
  name: 'group',
  children: [
    {
      name: 'group',
      title: '分组列表'
    },
    {
      name: 'group-detail',
      title: '分组详情页面'
    }
  ]
}]

// 模型信息左侧菜单栏数据
const modelList = [{
  title: '模型',
  icon: 'md-person',
  name: 'model',
  children: [
    {
      name: 'model',
      title: '模型列表'
    },
    {
      name: 'model-detail',
      title: '模型详情页面'
    }
  ]
}, {
  name: 'bladed',
  title: '叶片',
  icon: 'ios-people'
}, {
  title: '塔架',
  icon: 'ios-nuclear',
  name: 'tower',
  children: [
    {
      name: 'tower',
      title: '塔架列表'
    },
    {
      name: 'tower-detail',
      title: '塔架详情页面'
    }
  ]
}]

// 项目菜单数据
export const menuList = [{
  title: '用户设置',
  icon: 'ios-people',
  name: 'user-setting',
  children: userList
}, {
  title: '模型设置',
  icon: 'ios-nuclear',
  name: 'model-setting',
  children: modelList
}]

```
store/module/home.js
```
import { menuList } from './menu.js'

// 注释掉namespaced: true,
// namespaced: true,

//state添加:
state: {
  menuList: menuList,
  headerActiveName: 'user-setting', // 默认header选中菜单
  routerName: 'user' // 默认左侧选中菜单
}

//mutations添加:
mutations: {
  updateRouterName (state, routerName) {
    state.routerName = routerName
  },
  updateHeaderActiveName (state, headerActiveName) {
    state.headerActiveName = headerActiveName
  }
},

//actions添加:
actions: {
  updateHeaderActiveName ({ commit, state }, headerActiveName) {
    commit('updateHeaderActiveName', headerActiveName)
  },
  updateRouterName ({ commit, state }, routerName) {
    commit('updateRouterName', routerName)
  },
}
```
## kfc-global-container/views  测试页面
