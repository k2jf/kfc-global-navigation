<template>
  <Menu
    :active-name="$route.name"
    width="auto"
    @on-select="onChangeMenu">
    <template v-for="submenu in getMenuList">
      <MenuItem
        :name="submenu.name"
        v-if="!submenu.children"
        :key="submenu.title">
        <Icon :type="submenu.icon" />
        {{ submenu.title }}
      </MenuItem>
      <Submenu
        :name="submenu.name"
        v-if="submenu.children"
        :key="submenu.name">
        <template slot="title">
          <Icon :type="submenu.icon" />
          <span>{{ submenu.title }}</span>
        </template>
        <template v-for="child in submenu.children">
          <MenuItem :name="child.name" :key="'menuitem' + child.name">
            {{ child.title }}
          </MenuItem>
        </template>
      </Submenu>
    </template>
  </Menu>
</template>

<script>
import { Menu, MenuItem, Submenu, Icon } from 'iview'
export default {
  name: 'SiderMenu',
  components: {
    Menu,
    MenuItem,
    Submenu,
    Icon
  },
  computed: {
    getMenuList () {
      return this.$store.state.home.siderMenuList
    }
  },
  methods: {
    onChangeMenu (name) {
      // 跳转菜单对应页面
      this.$router.push({
        name: name
      })
      // 更新左侧高亮菜单名称
      this.$store.commit('updateRouterName', name)
    }
  }
}
</script>
