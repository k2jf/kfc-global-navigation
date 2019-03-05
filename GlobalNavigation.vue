<template>
  <div class="layout">
    <Layout class="layout-container">
      <GlobalHeader>
        <div slot="right-header">
          <GlobalMenu
            :menuList="getHeaderMenu"
            mode="horizontal"
            :isShowSubMenu="false"
            :activeName="getHeaderActiveName"
            theme="dark"
            @on-change="onHeaderMenuChange"></GlobalMenu>
        </div>
      </GlobalHeader>
      <div class="layout-content">
        <GlobalSider
          :menuList="getMenuList"
          style="float: left; height: 100%;"
          @on-change="onSiderMenuChange"
        />
        <Content :style="{padding: '24px', height: '100%', background: '#f5f7f9', float: 'right', width: 'calc(100% - 200px)'}">
          <keep-alive>
            <router-view></router-view>
          </keep-alive>
        </Content>
      </div>
    </Layout>
  </div>
</template>
<script>
import { Layout, Content } from 'iview'
import GlobalHeader from './components/GlobalHeader.vue'
import GlobalSider from './components/GlobalSider.vue'
import GlobalMenu from './components/GlobalMenu.vue'

export default {
  name: 'GlobalNavigation',
  components: {
    Layout,
    GlobalHeader,
    Content,
    GlobalSider,
    GlobalMenu
  },
  computed: {
    // 获取当前header菜单下对应作则菜单栏数据
    getMenuList () {
      let headerActiveName = this.getHeaderActiveName
      let menuList = this.getHeaderMenu
      return menuList.filter(item => item.name === headerActiveName)[0].children
    },
    // 获取header高亮菜单名称
    getHeaderActiveName () {
      return this.$store.state.home.headerActiveName
    },
    // 获取所有菜单数据
    getHeaderMenu () {
      return this.$store.state.home.menuList
    }
  },
  methods: {
    // 鼠标点击左侧菜单切换事件
    onSiderMenuChange (name) {
      // 跳转菜单对应页面
      this.$router.push({
        name: name
      })
      // 更新左侧高亮菜单名称
      this.$store.commit('updateRouterName', name)
    },
    // 鼠标点击header菜单切换事件
    onHeaderMenuChange (name) {
      // 更新header高亮菜单名称
      this.$store.commit('updateHeaderActiveName', name)
      // 获取当前header菜单对应左侧菜单数据
      let siderMenu = this.getHeaderMenu.filter(item => item.name === name)[0]
      // 获取切换header菜单后默认第一个菜单页面
      let siderActiveName = siderMenu.name
      // 如果是二级页面获取二级页面第一个页面
      if (siderMenu.children) {
        siderActiveName = siderMenu.children[0].name
      }
      // 更新左侧高亮菜单名称
      this.$store.commit('updateRouterName', siderActiveName)
      // 跳转页面
      this.$router.push({
        name: siderActiveName
      })
    }
  }
}
</script>
