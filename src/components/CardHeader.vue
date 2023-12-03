<script setup>
import { ref } from 'vue'
import BottomSheet from './BottomSheet.vue';
import CardsCarousel from './CardsCarousel.vue';

const props = defineProps({
  data: Object,
  cardDetails: Object
})

const emit = defineEmits(['addDebitCard', 'addCompanyCard', 'updateSelectedCard', 'freezeUnfreezeCard', 'removeCard'])

const tab = ref(1);

const createCardDialog = ref(false);
const cancelCardDialog = ref(false);

const cardName = ref('')
const cardIndexToCancel = ref(null)

function addNewDebitCard() {
  createCardDialog.value = true;
}
function closeDialog() {
  createCardDialog.value = false;
  cardName.value = '';
  cancelCardDialog.value = false;
}

function createCard() {
  if(cardName.value) {
    if(tab.value === 1) {
      emit('addDebitCard', cardName.value)
    } else {
      emit('addCompanyCard', cardName.value)
    }
    closeDialog();
  }
}

function updateSelectedCard(arg) {
  emit('updateSelectedCard', arg)
}

function freezeUnfreezeCard(arg) {
  emit('freezeUnfreezeCard', arg)
}

function removeCard(arg) {
  cancelCardDialog.value = true;
  cardIndexToCancel.value = arg;
  // emit('removeCard', arg)
}

function removeCardConfirm() {
emit('removeCard', cardIndexToCancel.value)
closeDialog();
}

function onTabChange(model) {
  const carousels = document.querySelectorAll('.carousel-wrapper');
  if(carousels.length) {
    const cardType = model === 1 ? 'debitCards' : 'companyCards';
    if(carousels.length >= model) {
    const selectedCardIndex = carousels[model - 1].getAttribute('data-model');
    emit('updateSelectedCard', props.data.cards[cardType][selectedCardIndex])
    } else {
      emit('updateSelectedCard', props.data.cards[cardType][0]);
    }
  }
}

</script>
 
<template>
  <div class="sticky">
    <header>
    <div class="top-header">
      <div class="balance-label">
        Account balance
      </div>
      <div class="logo icon"></div>
    </div>
    <div class="header-bottom">
      <div class="amount">
        <span class="currency">{{ data.currency }}</span>
        <span class="balance">{{ data.balance }}</span>
      </div>
      <div class="add-new-card cursor-pointer" @click="addNewDebitCard">
        <span class="icon add"></span>
        <span>New card</span>
      </div>
    </div>
  </header>
  <div class="card-tabs">
    <v-tabs v-model="tab" centered @update:modelValue="onTabChange">
      <v-tab :value="1" class="text-none">My debit cards</v-tab>
      <v-tab :value="2" class="text-none">All company cards</v-tab>
    </v-tabs>
    <v-window v-model="tab">

      <v-window-item
        :value="1"
      >
       <CardsCarousel :cards="data.cards.debitCards" @updateSelectedCard="updateSelectedCard"/>
      </v-window-item>
      <v-window-item
       :value="2"
      >
      <CardsCarousel :cards="data.cards.companyCards" @updateSelectedCard="updateSelectedCard"/>
      </v-window-item>
    </v-window>
  </div>
  </div>
  <BottomSheet :cardDetails="cardDetails" @freezeUnfreezeCard="freezeUnfreezeCard" @removeCard="removeCard"/>

  <template>
  <div class="text-center">
      <v-dialog
        v-model="createCardDialog"
        width="500"
      >
        <v-card>
          <v-text-field
              label="Enter card name"
              placeholder="Enter card name"
              type="text"
              v-model="cardName"
            ></v-text-field>
          <v-card-actions>
            <v-btn color="primary" @click="closeDialog">Close Dialog</v-btn>
            <v-btn color="primary"  @click="createCard">Create Card</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
  </div>
</template>

<template>
  <div class="text-center">
      <v-dialog
        v-model="cancelCardDialog"
        width="500"
      >
        <v-card>
          <h2>Are you sure you want to cancel the card?</h2>
          <v-card-actions>
            <v-btn color="primary" @click="closeDialog">Close Dialog</v-btn>
            <v-btn color="primary"  @click="removeCardConfirm">Cancel Card</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
  </div>
</template>
</template>

<style lang="scss">
header, .card-tabs {
  background: #0C365A;
  color: white;
  
}
header {
  padding: 24px;
}
.top-header {
  height: 56px;
  display: flex;
  justify-content: space-between;
  padding: 10px 0;

  .balance-label {
    font-size: 14px;
    font-weight: 500;
    align-self: end;
  }
  .logo {
    width: 25px;
    height: 25px;
    background-image: url('../assets/images/header-logo.svg');
  }
}
.header-bottom {
  display: flex;
  justify-content: space-between;
  .amount {
    display: flex;
    align-items: center;
  }
  .currency {
    font-size: 12px;
    background-color: #01D167;
    border-radius: 4px;
    padding: 5px 14px;
    font-weight: bold;
    margin-right: 10px;
  }
  .balance {
    font-size: 24px;
    font-weight: bold;
  }
  .add {
    width: 16px;
    height: 16px;
    background-image: url('../assets/images/add.svg');
    margin-right: 5px;
  }
  .add-new-card {
    color: #23CEFD;
    font-size: 13px;
    font-weight: bold;
    display: flex;
    align-items: center;
  }
}
.v-slide-group {
  .v-slide-group__container {
    padding: 0 24px;
    .v-tab {
      padding: 0;
      margin-right: 30px;
      font-size: 13px;
      opacity: 0.5;
      &.v-slide-group-item--active {
        font-weight: bold;
        opacity: 1;
      }
    }
    .v-slide-group-item--active .v-tab__slider{
      background-color: #23CEFD;
    }
  }
}

.sticky {
  position: fixed;
  width: 100%;
}
.v-overlay__content {
  .v-card {
    padding: 24px;
    .v-card-actions {
      justify-content: space-between;
    }
  }
}


</style>