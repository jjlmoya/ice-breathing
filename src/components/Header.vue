<template>
  <q-header>
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
          Quasar App
        </q-toolbar-title>
        <div>Quasar v{{ $q.version }}</div>
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
