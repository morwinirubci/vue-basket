<script >
export default {
  props: ['item', 'products', 'basketPosition', 'basketCount'],
  emits: ['remove-basket-item', 'change-basket-item', 'change-basket-count'],
  methods: {
    setItem(e) {
      this.products.forEach((item, idx) => {
        if(e.target.value === item.name){
          this.$emit('change-basket-item', this.basketPosition, idx);
        }
      })
    }
  },
}
</script>

<template>
  <tr :id="item.id">
    <td>
      <select @change="setItem" :value="item.name">
        <option 
        v-for="(item, idx) of products" 
        :key="idx" 
        :value="item.name">
          {{ item.name }}
        </option>
      </select>
    </td>
    <td>{{ item.price }}</td>
    <td>
      <input 
      type="number" 
      min="1" 
      step="1" 
      @input="$emit('change-basket-count', basketPosition, $event.target.value)" 
      :value="basketCount"/>
    </td>
    <td>
      <button class="basket__delete" @click="$emit('remove-basket-item', basketPosition)">Удалить</button>
    </td>
  </tr>
</template>
<style>
.basket__delete{
  position: relative;
  border: unset;
  color: #34495E;
  font-weight: 700;
  background: #ff5252;
  padding: 10px 15px;
  transition: .2;
  cursor: pointer;
  border-radius: 5px;
}
.basket__delete:hover{
  opacity: .8;
}
.basket__delete:active{
  top: 1px;
}
</style>

