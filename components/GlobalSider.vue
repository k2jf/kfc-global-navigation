<template>
  <Sider :style="{background: '#fff'}">
    <GlobalMenu
      :menuList="getMenuList"
      :isShowSubMenu="true"
      :activeName="getActiveName"
      theme="light"
      @on-change="onMenuChange" />
  </Sider>
</template>
<script>
import { Sider } from 'iview'
import GlobalMenu from './GlobalMenu.vue'
export default {
  name: 'GlobalSider',
  components: {
    Sider,
    GlobalMenu
  },
  props: {
    menuList: {
      type: Array,
      required: true
    }
  },
  computed: {
    getMenuList () {
      return this.menuList
    },
    getActiveName () {
      return this.$store.state.home.routerName
    }
  },
  methods: {
    onMenuChange (active) {
      this.$emit('on-change', active)
    }
  }
}
</script>
