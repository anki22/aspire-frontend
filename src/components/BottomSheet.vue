<script setup>
import { ref } from 'vue';
// import { reactive } from 'vue';

const props = defineProps({
  cardDetails: Object
})

const emit = defineEmits(['freezeUnfreezeCard', 'removeCard'])

function freezeUnfreezeCard() {
  emit('freezeUnfreezeCard', props.cardDetails.id);
}

function removeCard() {
  emit('removeCard', props.cardDetails.id);
}

const panels = ref(1)
</script>

<template>
<div class="bottom-sheet">
    <div class="card-actions">
      <div class="text-center cursor-pointer" @click="freezeUnfreezeCard">
        <span class="freeze icon"></span>
        <div>{{cardDetails.frozen ? 'Unfreeze' : 'Freeze'}} card</div>
      </div>
      <div class="text-center cursor-pointer">
        <span class="spend-limit icon"></span>
        <div>Set spend limit</div>
      </div>
      <div class="text-center cursor-pointer">
        <span class="gpay icon"></span>
        <div>Add to Gpay</div>
      </div>
      <div class="text-center cursor-pointer">
        <span class="replace icon"></span>
        <div>Replace card</div>
      </div>
      <div class="text-center cursor-pointer" @click="removeCard">
        <span class="cancel icon"></span>
        <div>Cancel card</div>
      </div>
    </div>
    <div class="expansion-panels">
      <v-expansion-panels v-model="panels">
        <v-expansion-panel>
          <v-expansion-panel-title>
            <div class="panel-title">
              <div class="panel-title-left">
              <span class="icon card-details"></span>
              <span>Card details</span>
              </div>
            </div>
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            <div class="transaction-list">
              <div v-for="(transaction, index) of cardDetails.transactions" :key="index" class="transaction">
                <div class="vendor">
                  <div class="vendor-icon"  :class="transaction.vendorType">
                  <span class="icon"></span>
                </div>
                <div class="vendor-details">
                  <span class="vendor-name">{{ transaction.vendor }}</span>
                  <span class="date">{{ transaction.date }}</span>
                  <span class="message">
                    <span class="card-icon-bg">
                      <span class="icon card-icon"></span>
                    </span>
                    <span>{{ transaction.type === 'credit' ? 'Refund on debit card' : 'Charged to debit card' }}</span>
                  </span>
                </div>
                </div>
                <div class="amount" :class="transaction.type === 'credit' && 'green'">
                  {{ transaction.type === 'credit' ? '+' : '-' }} {{ transaction.currency }} {{ transaction.amount }}
                  <span class="icon next cursor-pointer"></span>
                </div>
              </div>
            </div>
          </v-expansion-panel-text>
      </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-title>
            <div class="panel-title">
              <div class="panel-title-left">
              <span class="icon transactions"></span>
              <span>Recent transactions</span>
              </div>
            </div>
          </v-expansion-panel-title>
          <v-expansion-panel-text>
            <div class="transaction-list">
              <div v-for="(transaction, index) of cardDetails.transactions" :key="index" class="transaction">
                <div class="vendor">
                  <div class="vendor-icon"  :class="transaction.vendorType">
                  <span class="icon"></span>
                </div>
                <div class="vendor-details">
                  <span class="vendor-name">{{ transaction.vendor }}</span>
                  <span class="date">{{ transaction.date }}</span>
                  <span class="message">
                    <span class="card-icon-bg">
                      <span class="icon card-icon"></span>
                    </span>
                    <span>{{ transaction.type === 'credit' ? 'Refund on debit card' : 'Charged to debit card' }}</span>
                  </span>
                </div>
                </div>
                <div class="amount" :class="transaction.type === 'credit' && 'green'">
                  {{ transaction.type === 'credit' ? '+' : '-' }} {{ transaction.currency }} {{ transaction.amount }}
                  <span class="icon next cursor-pointer"></span>
                </div>
              </div>
            </div>
            <div class="view-all text-center cursor-pointer">View all card transactions</div>
          </v-expansion-panel-text>
      </v-expansion-panel>
      </v-expansion-panels>
    </div>
  </div>
</template>

<style lang="scss">
.bottom-sheet {
  background-color: #fff;
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  position: relative;
  top: 510px;
  padding-bottom: 120px;
  .card-actions {
    background-color: #EDF3FF;
    color: #0C365A;
    font-size: 13px;
    padding: 20px 15px;
    display: flex;
    justify-content: space-around;
    border-top-left-radius: 15px;
    border-top-right-radius: 15px;
    &>div {
      margin: 0 15px;
    }

    .freeze, .spend-limit, .gpay, .replace, .cancel {
      height: 32px;
      width: 32px;
    }
    .freeze {
      background-image: url('../assets/images/freeze.svg');
    }
    .spend-limit {
      background-image: url('../assets/images/spend-limit.svg');
    }
    .gpay {
      background-image: url('../assets/images/gpay.svg');
    }
    .replace {
      background-image: url('../assets/images/replace.svg');
    }
    .cancel {
      background-image: url('../assets/images/deactivate.svg');
    }
  }
  
  .transaction-list {
    padding: 16px;
    .transaction {
      display: flex;
      justify-content: space-between;
      padding: 16px 0;
      border-bottom: 1px solid #F5F5F5;
      &:last-child {
        border-bottom: none;
        padding-bottom: 0;
      }
      .vendor {
        display: flex;
      }
      .vendor-icon {
        display: inline-block;
        width: 48px;
        height: 48px;
        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-right: 12px;
        .icon {
          width: 16px;
          height: 16px;
        }
        &.file {
          background-color: #009DFF1A;
          .icon {
            background-image: url('../assets/images/file-storage.svg');
          }
        }
        &.announce {
          background-color: #F251951A;
          .icon {
            background-image: url('../assets/images/megaphone.svg');
          }
        }
        &.travel {
          background-color: #00D6B51A;
          .icon {
            background-image: url('../assets/images/flights.svg');
          }
        }
      }

      .vendor-details {
        display: flex;
        flex-direction: column;
        .vendor-name {
          color: #222222;
          font-size: 14px;
          font-weight: 600;
        }
        .date {
          font-size: 13px;
          color: #AAAAAA;
        }
        .message  {
          color: #325BAF;
          font-size: 12px;
          font-weight: 600;
          margin-top: 10px;
          .card-icon-bg {
            display: inline-flex;
            padding: 5px;
            border-radius: 50%;
            align-items: center;
            background-color: #325BAF;
            margin-right: 8px;
          }
          .card-icon {
            width: 10px;
            height: 8px;
            background-image: url('../assets/images/card.svg');
          }
        }
      }

      .amount {
        font-size: 14px;
        font-weight: bold;
        &.green {
        color: #01D167;
      }
      .next {
        width: 7px;
        height: 12px;
        background-image: url('../assets/images/next.svg');
        margin-left: 10px
      }
      }
    }
  }

  .view-all {
    background-color: #EDFFF5;
    border: 1px solid #DDFFEC;
    font-size: 13px;
    font-weight: 600;
    color: #01D167;
    padding: 15px;
    position: absolute;
    width: 100%;
    left: 0;
    border-bottom-left-radius: 8px;
    border-bottom-right-radius: 8px;
    bottom: -52px;
  }
  .expansion-panels {
    padding: 0 24px;
  }
  .v-expansion-panels {
    margin-top: 24px;
    .v-expansion-panel {
      border-radius: 8px;
      .v-expansion-panel-title {
        border-radius: 8px;
        background-color: #FAFCFF;
        border-bottom: 1px solid #F5F5F5;
        .v-expansion-panel-title__overlay {
          display: none;
        }
        .panel-title-left {
          display: flex;
          align-items: center;
          color: #0C365A;
          font-size: 14px;
          font-weight: 600;
          .icon.transactions {
            background-image: url('../assets/images/transactions.svg');
            width: 24px;
            height: 24px;
            margin-right: 12px;
          }
          .icon.card-details {
            background-image: url('../assets/images/card-details.svg');
            width: 24px;
            height: 24px;
            margin-right: 12px;
          }
        }
        .v-expansion-panel-title__icon {
          background-image: url('../assets/images/down-arrow.svg');
            width: 24px;
            height: 24px;
          i {
            display: none;
          }
        }
      }
      &.v-expansion-panel--active {
        .v-expansion-panel-title__icon {
          background-image: url('../assets/images/up-arrow.svg');
        }
      }
    }
  }
}
</style>
