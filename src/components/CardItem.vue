<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  card: Object
})
const show = ref(false);

function showCardNumber() {
  show.value = !show.value;
}

const cardNumber = computed(() => {
  let number = props.card.number;
  let numArray = number.split(' ');
  if(!show.value) {
    return numArray.map((el, i, arr) => i === arr.length - 1 ? el : '****' ).join(' ')
  } else {
    return numArray.join(' ')
  }
})
</script>

<template>
  <div class="row-wrap">
    <div class="card-wrapper">
    <div class="show-card-number cursor-pointer" @click="showCardNumber">
      <span class="icon eye"></span>
      <span>{{show ? 'Hide' : 'Show'}} card number</span>
    </div>
  <div class="card" :class="card.frozen ? 'frozen' : ''">
    
    <div class="text-right">
      <span class="icon aspire"></span>
    </div>
    <h3 class="name">{{ card.name }}</h3>
    <div class="number">
      {{ cardNumber }}
    </div>
    <div class="other-info">
      <span class="expiry">Thru: {{card.expiry}}</span>
      <span class="cvv">CVV: <span class="masked-cvv">***</span></span>
    </div>
    <div class="text-right">
      <span class="icon visa"></span>
    </div>
  </div>
  </div>
  </div>
  
  
</template>

<style lang="scss">
.row-wrap {
  display: flex;
  justify-content: center;
}
.card-wrapper {
  position: relative;
  max-width: 500px;
  flex: 1;
}
.card {
  height: 220px;
  background-color: #01D167;
  padding: 24px;
  margin: 50px 24px 24px;
  color: #fff;
  border-radius: 10px;
  position: relative;
  z-index: 2;

  .aspire{
    background-image: url('../assets/images/Logo.svg');
    height: 21px;
    width: 74px;
  }
  .visa {
    background-image: url('../assets/images/visa.svg');
    height: 20px;
    width: 59px;
  }

  .name {
    font-size: 22px;
    letter-spacing: 1px;
    margin: 12px 0;
  }

  .number {
    font-size: 14px;
    font-weight: 600;
    letter-spacing: 5px;
    margin-bottom: 15px;
  }

  .other-info {
    font-size: 14px;
    font-weight: 600;
    letter-spacing: 1px;
  }

  .expiry {
    margin-right: 30px;
  }

  .masked-cvv {
    font-size: 30px;
    vertical-align: -webkit-baseline-middle;
    line-height: 1;
  }
  &.frozen {
    background-color: grey;
  }
}
.show-card-number {
    background-color: white;
    color: #01D167;
    font-size: 12px;
    font-weight: bold;
    display: inline-flex;
    align-items: center;
    padding: 10px 10px 20px;
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;
    right: 24px;
    position: absolute;
    top: 15px;
    width: 150px;
    .eye {
      background-image: url('../assets/images/eye.svg');
      margin-right: 5px;
      height: 16px;
      width: 16px;
    }
  }
</style>
