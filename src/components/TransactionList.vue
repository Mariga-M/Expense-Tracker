<template>
     <h3>History</h3>
      <ul id="list" class="list">
        <li 
            v-for="transaction in transactions" 
            :key="transaction.id" 
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{transaction.text}} <span>${{ transaction.amount }}</span>
            <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
      </ul>
</template>


<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted'])

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    }
})

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
}

</script>


<!-- composition API explicit setup -->
<!-- <script>
export default{
   setup(){
    const transactions = [
        { id: 1, text: "Food", amount: -20.00 },
        { id: 2, text: "Salary", amount: 320.00 },
        { id: 3, text: "Picnic", amount: -97.00 },
        { id: 4, text: "Books", amount: -50.00 },
        { id: 5, text: "Side gig", amount: 80.00 },
    ];
    return{
        transactions
    }
   }
}
</script> -->


<!-- options API -->
<!-- <script>
export default{
    data(){
        return{
            transactions: [
                { id: 1, text: "Food", amount: -20.00 },
                { id: 2, text: "Salary", amount: 320.00 },
                { id: 3, text: "Picnic", amount: -97.00 },
                { id: 4, text: "Books", amount: -50.00 },
                { id: 5, text: "Side gig", amount: 80.00 },
            ],
        };
    },
}
</script> -->