<template>
  <div class="p-meditation">
    <Ground />
    <Meditation />
  </div>
</template>

<script>
import Ground from 'components/Ground.vue'
import Meditation from 'components/Meditation.vue'
export default {
  name: 'MyLayout',
  components: {
    Ground,
    Meditation
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
