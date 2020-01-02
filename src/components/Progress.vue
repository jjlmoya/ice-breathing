<template>
  <div class="progress">
   <q-circular-progress
      reverse
      :value="getValue()"
      size="90px"
      :thickness="0.2"
      color="light-blue"
      center-color="purple"
      track-color="white"
    />
    <div class="progress__content">{{value}}</div>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data: function () {
    return {
      state: 0,
      value: 35,
      breathNumber: 40,
      holdTime: 200,
      refreshTime: 15
    }
  },
  methods: {
    getTimeByState () {
      return this.state === 0
        ? this.breathNumber
        : this.state === 1
          ? this.holdTime
          : this.refreshTime
    },
    getValue () {
      return this.value * 100 / this.getTimeByState()
    }
  }
}
</script>
