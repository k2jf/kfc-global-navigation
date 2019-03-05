<template>
  <Menu
    :active-name="activeName"
    :mode="mode"
    :theme="theme"
    width="auto"
    @on-select="changeMenu"
  >
    <template v-for="submenu in getMenuList">
      <MenuItem
        :name="submenu.name"
        v-if="!submenu.children || !isShowSubMenu"
        :key="submenu.title">
        <Icon :type="submenu.icon" />
        {{ submenu.title }}
      </MenuItem>
      <Submenu
        :name="submenu.title"
        v-if="submenu.children && isShowSubMenu"
        :key="submenu.title">
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
  name: 'GlobalMenu',
  components: {
    Menu,
    MenuItem,
    Submenu,
    Icon
  },
  props: {
    menuList: {
      type: Array,
      required: true
    },
    isShowSubMenu: {
      type: Boolean,
      required: true
    },
    mode: {
      type: String,
      required: false,
      default: () => {
        return 'vertical'
      }
    },
    activeName: {
      type: String,
      required: true
    },
    theme: {
      type: String,
      required: true
    }
  },
  computed: {
    getMenuList () {
      return this.menuList
    }
  },
  methods: {
    changeMenu (active) {
      this.$emit('on-change', active)
    }
  }
}
</script>
