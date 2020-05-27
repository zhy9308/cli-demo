<template>
  <div class="bf-top-menu clearfix font-l">
    <span v-show="!item.hidden" v-for="item in constantRoutes" @click="toggleTopRouter(item, constantRoutes)" :class="item._topActive?'top-active color':''"  :key="item.path" v-if="item.meta&&item.meta.title">{{generateTitle(item.meta.title)}}</span>
  </div>
</template>

<script>
import { generateTitle } from '@/utils/i18n'
import { constantRoutes } from '@/router'
import store from '@/store'
import router from '@/router'
export default {
  data() {
    return {
      constantRoutes: constantRoutes
    }
  },
  mounted: function() {
    const history = sessionStorage.getItem('_topActive')
    if (history) {
      this.constantRoutes.some((v) => {
        if (v.name === history || v.path === history) {
          this.$set(v, '_topActive', true)
          store.dispatch('permission/FilterTopRoutes', v).then(() => {
            // router.addRoutes(store.getters.addRouters)
          })
          console.log(router)
          console.log(store.getters.addRouters)
          return false
        }
      })
    } else {
      this.$set(constantRoutes[6], '_topActive', true)
      store.dispatch('permission/FilterTopRoutes', constantRoutes[6]).then(() => {
        // router.addRoutes(store.getters.addRouters)
      })
    }
  },
  watch: {
    $route() {
      // console.log(this.$route)
    }
  },
  methods: {
    generateTitle,
    toggleTopRouter(item, list) {
      list.forEach((v) => {
        this.$set(v, '_topActive', false)
      })
      // sessionStorage.setItem('_topActive', item.name || item.path)
      sessionStorage.setItem('_topActive', item.name || item.path)
      this.$set(item, '_topActive', true)
      store.dispatch('permission/FilterTopRoutes', item).then(() => { // 根据roles权限生成可访问的路由表
        router.addRoutes(store.getters.addRouters) // 动态添加可访问路由表
      })
    },
    isActive(item) {
      return true
    }
  }
}
</script>

<style>
.bf-top-menu{
  float: left;
}
.bf-top-menu>span{
  margin: 0 7px;
  padding: 10px 7px;
  line-height: 46px;
  cursor: pointer;
}
.top-active{
  border-bottom: 2px solid #0099ff;
}
</style>
