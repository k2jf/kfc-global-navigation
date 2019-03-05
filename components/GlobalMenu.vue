<template>
  <Menu
    :active-name="getActiveName"
    mode="horizontal"
    theme="dark"
    width="auto"
    @on-select="changeMenu"
  >
    <template v-for="submenu in getMenuList">
      <MenuItem :name="submenu.name" :key="submenu.name">
        <Icon :type="submenu.icon" />
        {{ submenu.title }}
      </MenuItem>
    </template>
  </Menu>
</template>
<script>
import { Menu, MenuItem, Icon } from 'iview'
export default {
  name: 'GlobalMenu',
  components: {
    Menu,
    MenuItem,
    Icon
  },
  computed: {
    getMenuList () {
      return this.$store.state.home.headerMenuList
    },
    getActiveName () {
      return this.$store.state.home.headerActiveName
    }
  },
  methods: {
    changeMenu (active) {
      this.$emit('on-change', active)
    }
  }
}
</script>
