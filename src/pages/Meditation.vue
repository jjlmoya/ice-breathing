<template>
  <div class="p-meditation">
    <Progress />
    <Ground />
    <Meditation />
  </div>
</template>

<script>
import Ground from 'components/Ground.vue'
import Meditation from 'components/Meditation.vue'
import Progress from 'components/Progress.vue'

export default {
  name: 'MyLayout',
  components: {
    Ground,
    Meditation,
    Progress
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
