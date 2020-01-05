<template>
  <div class="progress">
      <div class="playing" v-if="this.round <= this.maxRounds">
      <div>Ronda {{round}} de {{maxRounds}}</div>
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
      <div class="progress__action"> {{action}} </div>
    </div>
    <div class="finish" v-if="!(this.round <= this.maxRounds)">
       <div class="progress__action">
         Meditación Acabada
       </div>
       <div class="progress__buttons">
       <q-btn v-on:click="restart"
          class="button"
          color="primary"
          label="Repetir"
          size="lg" />
       <q-btn to="/"
          class="button"
          color="primary"
          label="Volver"
          size="lg" />
        </div>
    </div>
  </div>
</template>
<script>

const breathIn = new Audio('statics/sounds/breath-in.mp3')
const breathOut = new Audio('statics/sounds/breath-out.mp3')
const ONE_SECOND = 1000
export default {
  name: 'Header',
  data: function () {
    return {
      state: 0,
      value: 0,
      breathNumber: 40,
      holdTime: 120,
      action: '',
      refreshTime: 15,
      maxRounds: 3,
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
      this.action = 'Aguanta'
      this.createLoop(this.holdTime, ONE_SECOND)
    },
    breathLoop () {
      const breathInDuration = 2.377
      const breathOutDuration = 1.337
      const durationSounds = (breathInDuration + breathOutDuration) * ONE_SECOND
      this.round++
      if (this.round <= this.maxRounds) {
        this.createLoop(this.breathNumber, durationSounds, () => {
          breathIn.play()
          this.action = 'Inspira'
          setTimeout(() => {
            this.action = 'Expira'
            breathOut.play()
          }, breathInDuration * ONE_SECOND)
        })
      } else {

      }
    },
    refreshLoop () {
      this.action = '¡Inspira hondo y Aguanta!'
      this.createLoop(this.refreshTime, ONE_SECOND)
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
        if (this.value > max) {
          clearInterval(loop)
          this.state = this.state !== 2 ? this.state + 1 : 0
          this.value = 0
          this.nextLoop()
        } else {
          if (callback) callback()
        }
      }, step)
    },
    restart () {
      this.round = 0
      this.nextLoop()
    }
  }
}
</script>
