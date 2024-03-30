<script >
import BasketItem from './components/BasketItem.vue'
export default {
  components: {
    BasketItem
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Картофель', price: 20 },
        { id: 2, name: 'Сок', price: 100 },
        { id: 3, name: 'Мясо', price: 500 },
        { id: 4, name: 'Бананы', price: 50 }
      ],
      basket: []
    }
  },
  methods: {
    addNewProduct() {
      this.basket.push({ product: this.products[0], count: 1 });
    },
    removeBusketItem(id) {
      this.basket.splice(id, 1);
    },
    changeBasketItem(idx, id) {
      this.basket[idx].product = this.products[id];
    },
    changeBasketCount(idx, count) {
      this.basket[idx].count = count;
    }
  },
  computed: {
    fullprice() {
      let sum = 0;
      this.basket.forEach((item) => {
        sum += item.product.price * item.count;
      })
      return sum;
    }
  }
}
</script>

<template>
  <div class="basket">
    <p class="basket__title">Корзина</p>
    <button class="basket__btn" @click="addNewProduct">Добавить</button>
    <table class="basket__table">
      <tr>
        <th>Товар</th>
        <th>Стоимость</th>
        <th>Количество</th>
        <th></th>
      </tr>
      <BasketItem
        v-for="(item, idx) in basket"
        :key="idx"
        :item="item.product"
        :basketPosition="idx"
        :basketCount="item.count"
        :products="products"
        @remove-basket-item="removeBusketItem"
        @change-basket-item="changeBasketItem"
        @change-basket-count="changeBasketCount"
      />
      <tr class="basket__total">
        <td></td>
        <td>ИТОГО:</td>
        <td>{{ fullprice > 1 ? fullprice : 0 }}</td>
        <td></td>
      </tr>
    </table>
  </div>
</template>

<style>
body {
  font-family: 'Montserrat', sans-serif;
  background: #3e4e5e1c;
}
table {
  border-radius: 5px;
}
table,
td,
th {
  border: 5px solid #34495e;
  border-collapse: collapse !important;
  color: #34495e;
  font-weight: 600;
}
td,
th {
  padding: 10px 20px;
  text-align: center;
  min-width: 100px;
}
input,
select {
  width: 100%;
  border: unset;
  outline: unset;
  padding: 10px 5px;
  font-family: 'Montserrat', sans-serif;
  border-radius: 5px;
  font-weight: 600;
  background: transparent;
  cursor: pointer;
  font-size: 18px;
  color: #34495e;
}
input {
  text-align: center;
  border-bottom: 1px solid;
  border-radius: unset;
}
button {
  font-family: 'Montserrat', sans-serif;
}
.basket {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  max-width: 1000px;
  margin: 0 auto;
}
.basket__title {
  font-size: 34px;
  margin: 20px 0;
  font-weight: 700;
  color: #34495e;
}
.basket__btn {
  position: relative;
  border: unset;
  background-color: #41b883;
  padding: 15px 30px;
  color: #34495e;
  font-weight: 700;
  border-radius: 5px;
  transition: 0.2s;
  cursor: pointer;
}
.basket__btn:hover {
  background-color: #34495e;
  color: #41b883;
}
.basket__btn:active {
  top: 1px;
}
.basket__total td {
  font-weight: 700;
  font-size: 22px;
}
</style>
