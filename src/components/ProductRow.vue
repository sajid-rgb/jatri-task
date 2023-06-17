<script setup>
    const props = defineProps(['item','index','productId','currentPage']);
    const emit = defineEmits(['get-product','empty-product']);

    //this is dynamic serial no. this serial no will not changed when sorting.
    const getSerialNo = () => (props.currentPage - 1)*5+ props.index + 1;

</script>
<template>
    <tr :key="props.item.id">
                <td>{{ getSerialNo() }}</td>
                <td>{{ props.item.title }}</td>
                <td>{{ props.item.rating }}</td>
                <td>{{ props.item.price }}</td>
                <td>
                    <div class="button-div">
                        <button class="show-button" @click="emit('get-product',props.item.id)" v-if="props.item.id !== props.productId">Show</button>
                        <button class="close-button" @click="emit('empty-product')" v-else>Close</button>
                    </div>
                </td>
            </tr>
</template>


<style scoped>
.table th,
.table td {
  width: 20%;
  padding: 8px;
  border: 1px solid #ccc;
}
.button-div{
    display: flex;
    align-items: center;
    justify-content: center;
}
.show-button, .close-button{
    border: none;
    height: 35px;
    width: 100px;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}
.show-button{
    background-color:#70ad47;
}
.close-button{
    background-image: linear-gradient(#e76e1b,#f28748)
}
</style>