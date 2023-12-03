<script setup>
import { ref, watch } from 'vue';
import CardItem from './CardItem.vue';


const props = defineProps({
  cards: Object
})

const emit = defineEmits(['updateSelectedCard'])

const model = ref(0);

watch(model, async (newmodel) => {
  emit('updateSelectedCard', props.cards[newmodel])
})
</script>

<template>
  <div class="carousel-wrapper" :data-model="model">
   <v-carousel
    :model-value="model"
    v-model="model"
    height="320"
    :show-arrows="false"
    hide-delimiter-background
    delimiter-icon="mdi-circle"
  >
    <v-carousel-item
      v-for="(card, i) in cards"
      :key="i"
    >
      <CardItem :card="card"/>
    </v-carousel-item>
  </v-carousel>
  </div>
</template>

<style lang="scss">
.carousel-wrapper {
  .v-carousel__controls {
    .v-btn__overlay, .v-underlay {
      display: none;
    }
    .v-btn {
      margin: 0;
      .v-btn__content {
        display: inline-block;
        height: 8px;
        width: 8px;
        border-radius: 8px;
        background-color: #01D167;
        opacity: 0.1;

        .v-icon {
          display: none;
        }
      }
    }
    .v-btn--active {
      .v-btn__content {
        opacity: 1;
        width: 16px;
      }
      
    }
  }
}
</style>
