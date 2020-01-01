<template>
  <q-layout view="lHh Lpr lFf">
    <Header :leftDrawerOpen="leftDrawerOpen" @setStatus="setMenuStatus" />
    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-2"
    >
     <Menu/>
    </q-drawer>

    <q-page-container>
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
      console.log('statuts %o', status)
      this.leftDrawerOpen = status
    }
  }
}
</script>
