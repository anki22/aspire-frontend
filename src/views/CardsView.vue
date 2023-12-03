<script setup>
import { reactive, ref } from 'vue';
import CardHeader from '../components/CardHeader.vue'
import PageMenu from '../components/PageMenu.vue'
import { v4 as uuidv4 } from 'uuid';


let rawData = localStorage.getItem('data') && JSON.parse(localStorage.getItem('data'));
if(!rawData) {
  rawData = {
  balance: '3,000',
  currency: 'S$',
  cards: {
    debitCards: [
      {
        name: 'Mark Henry 1',
        number: "1234 5678 2345 2020",
        expiry: '12/24',
        company: 'visa',
        frozen: false,
        id: 1,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry 2',
        number: "1234 5678 2345 3214",
        expiry: '08/26',
        company: 'visa',
        frozen: true,
        id: 2,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry 3',
        number: "1234 5678 2345 5463",
        expiry: '12/25',
        company: 'visa',
        frozen: false,
        id: 3,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      }
    ],
    companyCards: [
      {
        name: 'Mark Henry Office 1',
        number: "1234 5678 2345 2020",
        expiry: '12/24',
        company: 'visa',
        frozen: false,
        id: 4,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry Office 2',
        number: "1234 5678 2345 3214",
        expiry: '08/26',
        company: 'visa',
        frozen: false,
        id: 5,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry Office 3',
        number: "1234 5678 2345 5463",
        expiry: '12/25',
        company: 'visa',
        frozen: false,
        id: 6,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry Office 4',
        number: "1234 5678 2345 2020",
        expiry: '12/24',
        company: 'visa',
        frozen: false,
        id: 7,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
      {
        name: 'Mark Henry Office 5',
        number: "1234 5678 2345 2020",
        expiry: '12/24',
        company: 'visa',
        frozen: false,
        id: 8,
        transactions: [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
        ]
      },
    ]
  }
}
localStorage.setItem('data', JSON.stringify(rawData))
}
const data = reactive(rawData);



const dummyTransactions =  [
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "file"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'debit',
            currency: 'S$',
            amount: '150',
            vendorType: "travel"
          },
          {
            vendor: 'Hamleys', 
            date: '20 May 2020',
            type: 'credit',
            currency: 'S$',
            amount: '150',
            vendorType: "announce"
          }
];

const dummyCard = {
    number: "1234 5678 2463 2020",
    expiry: '12/24',
    company: 'visa',
    frozen: false,
    transactions: dummyTransactions,
    id: uuidv4()
}

const cardDetails = ref(data.cards.debitCards[0]);

function addDebitCard(cardName) {
  const card = dummyCard;
  card.name = cardName;
  data.cards.debitCards.unshift(card);
  cardDetails.value = card;
  localStorage.setItem('data', JSON.stringify(data))
}

function addCompanyCard(cardName) {
  const card = dummyCard;
  card.name = cardName;
  data.cards.companyCards.unshift(card);
  cardDetails.value = card;
  localStorage.setItem('data', JSON.stringify(data))
}

function updateSelectedCard(card) {
  cardDetails.value = card;
}

function freezeUnfreezeCard(id) {
  let el = data.cards.debitCards.find(el => el.id === id) || data.cards.companyCards.find(el => el.id === id);
  el.frozen = !el.frozen;
  localStorage.setItem('data', JSON.stringify(data))
}

function removeCard(id) {
  let index = data.cards.debitCards.findIndex((el) => el.id === id);
  if(index !== -1) {
    data.cards.debitCards.splice(index, 1)
  } else {
    let index = data.cards.companyCards.findIndex((el) => el.id === id);
    index !== -1 && data.cards.companyCards.splice(index, 1)
  }
  localStorage.setItem('data', JSON.stringify(data))
}
</script>

<template>
  <main>
    <CardHeader 
      :data="data" 
      @addDebitCard="addDebitCard" 
      :cardDetails="cardDetails" 
      @updateSelectedCard="updateSelectedCard"
      @freezeUnfreezeCard="freezeUnfreezeCard"
      @removeCard="removeCard"
      @addCompanyCard="addCompanyCard"
    />
    <PageMenu />
  </main>
</template>
