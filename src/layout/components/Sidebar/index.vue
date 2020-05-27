<template>
  <div :class="{'has-logo':showLogo}">
    <logo v-if="showLogo" :collapse="isCollapse" />
    <el-scrollbar wrap-class="scrollbar-wrapper">
      <el-menu
        :default-active="activeMenu"
        :collapse="isCollapse"
        :background-color="variables.menuBg"
        :text-color="variables.menuText"
        :unique-opened="false"
        :active-text-color="variables.menuActiveText"
        :collapse-transition="false"
        mode="vertical"
      >
      <div class="1" v-if="menuType=='left'">
        <sidebar-item v-for="route in permission_routes" :menuType="menuType" :key="route.path" :item="route" :base-path="route.path" :topRouters="topRouters" :topRoutersData="topRoutersData" />
      </div>
      <div class="2" v-if="menuType=='top'">
        <sidebar-top v-for="route in topRouters" :menuType="menuType" :key="route.path" :item="route" :base-path="route.path" :topRouters="topRouters" :topRoutersData="topRoutersData" />
      </div>
      </el-menu>
    </el-scrollbar>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Logo from './Logo'
import SidebarItem from './SidebarItem'
import SidebarTop from './SidebarTop'
import variables from '@/styles/variables.scss'

export default {
  props: ['menuType'],
  components: { SidebarItem, Logo, SidebarTop },
  computed: {
    ...mapGetters([
      'permission_routes',
      'sidebar',
      'topRouters',
      'topRoutersData'
    ]),
    activeMenu() {
      const route = this.$route
      const { meta, path } = route
      // if set path, the sidebar will highlight the path you set
      if (meta.activeMenu) {
        return meta.activeMenu
      }
      return path
    },
    showLogo() {
      return this.$store.state.settings.sidebarLogo
    },
    variables() {
      return variables
    },
    isCollapse() {
      return !this.sidebar.opened
    }
  },
  mounted() {
    
  },
}
</script>
