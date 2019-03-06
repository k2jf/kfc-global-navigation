<template>
  <div class="layout">
    <Layout class="layout-container">
      <GlobalHeader>
        <div slot="right-header">
          <GlobalMenu @on-change="onHeaderMenuChange"></GlobalMenu>
        </div>
      </GlobalHeader>
      <div class="layout-content">
        <GlobalSider style="float: left; height: 100%;" />
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
    // 获取所有菜单数据
    getHeaderMenu () {
      return this.$store.state.home.menuList
    }
  },
  methods: {
    // 鼠标点击header菜单切换事件
    onHeaderMenuChange (name) {
      const getActiveName = (menuList) => {
        if (menuList.children) {
          return getActiveName(menuList.children[0])
        }
        return menuList.name
      }
      // 更新header高亮菜单名称
      this.$store.commit('updateHeaderActiveName', name)
      // 获取当前header菜单对应左侧菜单数据
      let siderMenu = this.getHeaderMenu.filter(item => item.name === name)
      // 获取切换header菜单后默认第一个菜单页面
      let siderActiveName = getActiveName(siderMenu[0])
      // 更新左侧高亮菜单名称
      this.$store.commit('updateRouterName', siderActiveName)
      // 更新左侧菜单数据
      this.$store.commit('updateSiderMenuList', siderMenu[0].children)
      // 跳转页面
      this.$router.push({
        name: siderActiveName
      })
    }
  }
}
</script>
