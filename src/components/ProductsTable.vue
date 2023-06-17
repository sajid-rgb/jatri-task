<script setup>
    import { computed,ref } from 'vue';
    import { tableData } from '../helpers/uiData';
    import ProductRow from './ProductRow.vue';
    import ProductDetails from './ProductDetails.vue';

    const props = defineProps(['data','selectedOption','product','currentPage']);
    const product = ref({});

    //this method used  for sorted ascending/descending order when sort button changed
    const sortedData = computed(() =>{
        if(props.selectedOption.name === 'Ascending'){
            return props.data.sort((prev, next) => prev[props.selectedOption.key] - next[props.selectedOption.key]);
        } else  if(props.selectedOption.name === 'Descending'){
            return props.data.sort((prev, next) => next[props.selectedOption.key] - prev[props.selectedOption.key]);
        } else {
            return props.data;
        }
    } );

    //this method get all single product and set it to product variable
    const handleGetProduct = (id) => {
        fetch(`https://dummyjson.com/products/${id}`)
        .then(response => response.json())
        .then(result=> {
            product.value = result;
        })
        .catch(err => {
            console.log(err);
        })
    };

    //this method is used for clearing data after close button clicked
    const handleEmptyProduct = () => product.value = {};

</script>
<template>
    <div class="table-container" v-if="sortedData.length">
        <table class="table">
            <thead>
            <tr>
                <th v-for="item in tableData" :key="item.id">{{ item.title }}</th>
            </tr>
            </thead>
            <tbody v-for="(item,index) in sortedData">
                <ProductRow :item="item" :index="index" :productId="product.id" :currentPage="props.currentPage" @empty-product="handleEmptyProduct" @get-product="handleGetProduct" />
                <ProductDetails :product="product" :itemId="item.id" />
            </tbody>
        </table>
    </div>
</template>


<style scoped>
.table-container {
  width: 100%;
  overflow-x: auto;
}

.table {
  width: 60%;
  margin: auto;
  border-collapse: collapse;
}

.table th,
.table td {
  width: 20%;
  padding: 8px;
  border: 1px solid #ccc;
}
.table th {
  background-color: #f0f0f0;
  font-weight: bold;
}

.table tr:nth-child(even) {
  background-color: #f9f9f9;
}

</style>