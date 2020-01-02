<template>
  <div class="progress">
    <div>Ronda {{round}}</div>
    <div class="progress__wrapper">
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
  </div>
</template>

<script>
export default {
  name: 'Header',
  data: function () {
    return {
      state: 0,
      value: 0,
      breathNumber: 40,
      holdTime: 120,
      refreshTime: 15,
      max: 0,
      round: 0
    }
  },
  mounted () {
    this.nextLoop()
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
    },
    holdLoop () {
      this.createLoop(this.holdTime, 100)
    },
    breathLoop () {
      this.createLoop(this.breathNumber, 200)
      this.round++
    },
    refreshLoop () {
      this.createLoop(this.refreshTime, 100)
    },
    nextLoop () {
      switch (this.state) {
        case 0:
          this.breathLoop()
          break
        case 1:
          this.holdLoop()
          break
        case 2:
          this.refreshLoop()
          break
      }
    },
    createLoop (max, step) {
      console.log(max)
      let loop = setInterval(() => {
        this.value++
        if (this.value >= max) {
          clearInterval(loop)
          this.state = this.state !== 2 ? this.state + 1 : 0
          this.value = 0
          this.nextLoop()
        }
      }, step)
    }
  }
}
</script>
