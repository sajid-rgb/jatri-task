<script setup>
    import { onMounted, ref, watch } from 'vue';
    import Dropdown from '../components/Dropdown.vue';
    import { options }  from '../helpers/uiData'
    import ProductsTable from '../components/ProductsTable.vue';
    import Pagination from '../components/pagination.vue';

    const selectedData = ref({});
    const data = ref([]);
    const total = ref(0);
    const skip = ref(0);
    const currentPage = ref(1);

    //this method stores selected data for sorting
    const handleSelection = (value,context) => selectedData.value = {name: value, key: context};

    //this method will call when user click any page
    const handlePageChange = (page) => {
        currentPage.value = page;
        skip.value = (page-1)*5;
    };

    //this method will call when user click next button in pagination
    const handleNextPage = () => {
        currentPage.value += 1;
        skip.value = (currentPage.value-1)*5;
    }

    //this method will call when user click previous button in pagination
    const handlePrevPage = () => {
        currentPage.value -= 1;
        skip.value = (currentPage.value-1)*5;
    }

    //this method gets all products data from api
    const getData = (key) => {
        fetch(`https://dummyjson.com/products?limit=5&skip=${skip.value}`)
        .then(response => response.json())
        .then(result => {
            data.value = result.products;
            if(key === 'initial') {
                total.value = result.total;
            }
        })
        .catch(err => {
            console.log(err);
        })
    }
    
    //when skip change api will call, this watch used for it.
    watch(skip, ()=> {
        getData('')
    })

    //we use it for first time api calling
    onMounted(() => {
        getData('initial')
    })

</script>

<template>
   <header class="sorting-dropdown" >
        <Dropdown :data="options" :label="'Price'" :context="'price'" @change="handleSelection" />
        <Dropdown :data="options" :label="'Ratings'" :context="'rating'" @change="handleSelection" />
   </header>

  <main class="table-container">
    <ProductsTable :data="data" :selectedOption="selectedData" :currentPage="currentPage" />
    <Pagination :total="total" :skip="skip" :currentPage="currentPage" @on-click="handlePageChange" @next-page="handleNextPage" @prev-page="handlePrevPage"/>
  </main>
</template>
<style scoped>
.table-container {
  width: 100%;
  overflow-x: auto;
}
.sorting-dropdown{
    display: flex;
    justify-content: flex-end;
    margin-right: 20%;
    margin-bottom: 1%;
    margin-top: 1%;
    gap:10px;
}

</style>
