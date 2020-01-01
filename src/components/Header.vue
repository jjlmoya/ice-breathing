<template>
  <q-header class="header">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="changeMsg"
          icon="menu"
          aria-label="Menu"
        />
        <q-toolbar-title>
           Ice Breath
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
</template>

<script>
export default {
  name: 'Header',
  data: function () {
    return {
      leftDrawerOpen: this.leftDrawerOpen
    }
  },
  methods: {
    changeMsg () {
      this.leftDrawerOpen = true
      this.$emit('setStatus', this.leftDrawerOpen)
    }
  }
}
</script>
