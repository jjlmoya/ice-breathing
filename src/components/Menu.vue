<template>
   <q-list>
    <q-item-label header>Menú</q-item-label>
    <Item :title="'Inicio'" :icon="'home'" :link="'/'" />
    <Item :title="'Configuración'" :icon="'settings'" :link="'/'" />
    <Item :title="'Soporte'" :subtitle="''" :icon="'€'" :link="'/'" />
  </q-list>
</template>

<script>
import Item from 'components/Item.vue'
export default {
  name: 'Menu',
  components: {
    Item
  }
}
</script>
