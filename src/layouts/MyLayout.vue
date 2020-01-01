<template>
  <q-layout view="lHh Lpr lFf" class="l-meditation">
    <Header :leftDrawerOpen="leftDrawerOpen" @setStatus="setMenuStatus" />
    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
       class="menu"
      content-class="bg-grey-2"
    >
     <Menu/>
    </q-drawer>

    <q-page-container class="l-meditation__container">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import Header from 'components/Header.vue'
import Menu from 'components/Menu.vue'
export default {
  name: 'MyLayout',
  components: {
    Header,
    Menu
  },

  data () {
    return {
      leftDrawerOpen: false
    }
  },
  methods: {
    setMenuStatus (status) {
      this.leftDrawerOpen = status
    }
  }
}
</script>
