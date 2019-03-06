<template>
  <Sider :style="{background: '#fff'}">
    <SiderMenu />
  </Sider>
</template>

<script>
import { Sider } from 'iview'
import SiderMenu from './SiderMenu.vue'

export default {
  name: 'GlobalSider',
  components: {
    Sider,
    SiderMenu
  }
}
</script>
