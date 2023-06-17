<script setup>
import { ref } from 'vue';

const props = defineProps(['data','label','context']);
const emit = defineEmits(['change'])
const selectedOption = ref(props.data[0].label);

//this method will call when any option change in dropdown
const handleChange=()=>emit('change',selectedOption,props.context);

</script>

<template>
    <div class="dropdown">
        <label>{{ props.label }}</label>
        <select class="dropdown-select" v-model="selectedOption" @change="handleChange">
            <option v-for="item in props.data" :value="item.label" :key="item.value">{{ item.label }}</option>
        </select>
    </div>
</template>


<style scoped>
.dropdown {
  display: inline-block;
}

.dropdown-select {
  padding: 8px;
  font-size: 14px;
  border-radius: 4px;
  cursor: pointer;
}

select {
    width: 120px;
    padding: 5px;
    font-size: 16px;
    line-height: 1;
    border: 1px solid rgb(209, 201, 201);
    border-radius: 5px;
    height: 34px;
    background: white;
    appearance: none;
    background-position-x: 244px;
    margin-left: 5px;
}

label{
    font-size: 18px;
}

option{
    font-size: 18px;
}
</style>