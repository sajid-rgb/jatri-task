<script setup>
import { computed } from 'vue';
const props = defineProps(['total','skip','currentPage']);
const emit = defineEmits(['on-click','next-page','prev-page']);
const itemsPerPage = 5;

//it calculates the total pages for pagination
const totalPages = computed(() => Math.ceil(props.total / itemsPerPage));

</script>
<template>
    <div class="pagination" v-if="totalPages">
        <button class="prev" @click="emit('prev-page')" :disabled="props.currentPage === 1">Prev</button>
        <button
        v-for="page in totalPages"
        :key="page"
        @click="emit('on-click',page)"
        :disabled="props.currentPage === page"
      >
        {{ page }}
      </button>
      <button class="next" @click="emit('next-page')" :disabled="props.currentPage === totalPages">Next</button>
    </div>
</template>


<style scoped>
.pagination{
    margin-top: 10px;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}

.pagination button{
    background-color: white;
    height: 20px;
    width: 30px;
    border: 1px solid green;
    margin-left: 5px;
    border-radius: 20px;
    cursor: pointer;
}

.pagination button[disabled]{
    background-color: green;
    color: white;
}
.prev,.next{
    width: 80px !important;
    height: 30px !important;
    border-radius: 2px;
    background-color: white;
}
.prev:hover,.next:hover{
    background-color: green;
    color: white;
}

.prev[disabled],.next[disabled]{
    background-color: gray !important;
}

</style>