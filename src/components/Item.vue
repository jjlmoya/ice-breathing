<template>
  <q-item clickable :tag="tag" :href="link">
    <q-item-section avatar>
      <q-icon :name="icon" />
    </q-item-section>
    <q-item-section>
      <q-item-label>{{title}}</q-item-label>
      <q-item-label v-if="subtitle" caption>{{subtitle}}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
export default {
  name: 'Header',
  props: {
    icon: {
      type: String,
      default: 'home'
    },
    title: {
      type: String,
      default: ''
    },
    subtitle: {
      type: String,
      default: ''
    },
    link: {
      type: String,
      default: ''
    },
    tag: {
      type: String,
      default: 'a'
    }
  }
}
</script>
