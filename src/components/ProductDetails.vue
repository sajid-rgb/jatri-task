<script setup>
const props = defineProps(['product','itemId'])
</script>
<template>
    <tr class="details-row" v-if="props.product.id && props.product.id === props.itemId">
               <td colspan="5">
                  <div>
                     <h3>Details View</h3>
                     <h3>...............................</h3>
                     <p>Name: {{ props.product.title }}</p>
                     <p>Price: {{ props.product.price}}</p>
                     <p>Rating: {{ props.product.rating }}</p>
                     <p>Description: {{ props.product.description }}</p>
                  </div>
               </td>
            </tr>
</template>


<style scoped>
.table td {
  width: 20%;
  padding: 8px;
  border: 1px solid #ccc;
}
.details-row{
    background-color: white !important;
}

.details-row h3 {
    text-align: center;
    font-weight: normal;
}


.details-row p {
    margin-left: 20px;
}

.details-row td {
    padding: 20px 0 !important;
}
.details-row td div {
    width: 100%;
    border: 2px solid #5c85aa;
    border-radius: 30px;
    background-image: linear-gradient(#fefefe,#e9e9e9);
}
</style>