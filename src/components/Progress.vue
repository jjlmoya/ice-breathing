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

const breathIn = new Audio('statics/sounds/breath-in.mp3')
const breathOut = new Audio('statics/sounds/breath-out.mp3')

export default {
  name: 'Header',
  data: function () {
    return {
      state: 0,
      value: 0,
      breathNumber: 3,
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
      const breathInDuration = 2.377
      const breathOutDuration = 2.037
      const durationSounds = (breathInDuration + breathOutDuration) * 1000
      this.round++
      this.createLoop(this.breathNumber, durationSounds, () => {
        breathIn.play()
        setTimeout(() => {
          breathOut.play()
        }, breathInDuration * 1000)
      })
    },
    refreshLoop () {
      this.createLoop(this.refreshTime, 1000)
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
    createLoop (max, step, callback) {
      if (callback) { callback() }
      let loop = setInterval(() => {
        this.value++
        if (this.value >= max) {
          clearInterval(loop)
          this.state = this.state !== 2 ? this.state + 1 : 0
          this.value = 0
          this.nextLoop()
        } else {
          if (callback) callback()
        }
      }, step)
    }
  }
}
</script>
