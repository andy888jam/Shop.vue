<template>
  <div class="container main__cart">
    <div class="main__cart-title cellphone">
      <h5 class="main__cart-title-text">購物籃</h5>
    </div>
    <!-- cart items -->
    <div class="main__cart__items">
      <div class="main__cart__items__item" v-for="item in items" :key="item.id">
        <div class="item-picture">
          <img :src="item.img" alt="" />
        </div>
        <div class="item-detail">
          <div class="detail-left">
            <p class="item-name">{{ item.name }}</p>
            <div class="numbers">
              <button
                class="item-detail__numbers__minus"
                @click="removeItem(item.id)"
              >
                -
              </button>
              <p class="item-detail__numbers__number">{{ item.quantity }}</p>
              <button
                class="item-detail__numbers__plus"
                @click="addItem(item.id)"
              >
                +
              </button>
            </div>
          </div>
          <div class="item-price">${{ item.price }}</div>
        </div>
      </div>
    </div>
    <div class="main__cart__delivery">
      <p>運費</p>
      <p>{{ passPrice }}</p>
    </div>
    <div class="main__cart__total">
      <p>小計</p>
      <p class="total-price">＄{{ this.total }}</p>
    </div>
  </div>
</template>

<script>
import picURL1 from "@/assets/Block@2x.png";
import picURL2 from "@/assets/Block2@2x.png";
const dummyItems = [
  {
    id: 1,
    img: picURL1,
    name: "破壞補丁修身牛仔褲",
    price: 3999,
    quantity: 1,
  },
  {
    id: 2,
    img: picURL2,
    name: "刷色直筒牛仔褲",
    price: 1299,
    quantity: 1,
  },
];
export default {
  props: ["passPrice"],
  data() {
    return {
      items: [],
      total: Number,
    };
  },
  methods: {
    fetchFeeds() {
      this.items = dummyItems;
      console.log(this.items);
    },
    addItem(id) {
      this.items.forEach((item) => {
        if (item.id === id) {
          item.quantity++;
          this.calTotal();
        }
      });
    },
    removeItem(id) {
      this.items.forEach((item) => {
        if (item.id === id && item.quantity > 1) {
          item.quantity--;
          this.calTotal();
        }
      });
    },
    calTotal() {
      const totalArray = [];
      this.items.forEach((item) => {
        totalArray.push(item.price * item.quantity);
      });
      this.total = totalArray.reduce((a, b) => a + b, 0);
      if (this.passPrice === "免費") {
        return;
      } else {
        this.total += 500;
      }
    },
  },
  watch: {
    passPrice: function () {
      this.calTotal();
    },
  },
  created() {
    this.fetchFeeds();
    this.calTotal();
  },
};
</script>

<style scope>
/* 初始設定 */
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
}
h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0px;
  padding: 0px;
}
ul,
ol,
li {
  list-style: none;
  margin: 0px;
  padding: 0px;
}
a,
a:hover,
a:focus {
  text-decoration: none;
  color: black;
}
img {
  width: 100%;
  height: 100%;
  display: block;
}
.btn,
button,
button:focus,
input:focus,
textarea:focus,
select,
select:focus,
a:focus {
  outline: 0px !important;
}
button {
  background-color: transparent;
  border: 0;
  cursor: pointer;
}
button[disabled] {
  pointer-events: none;
}
input {
  padding: 0;
}
input:required {
  box-shadow: none;
}
input:invalid {
  box-shadow: none;
}

/* 商品細節設定 */
.item-picture {
  width: 100px;
  height: 100px;
}
.item-picture img {
  width: 100%;
  height: 100%;
}
.main__cart {
  border-radius: 4px;
  border: 1px solid #f0f0f5;
  margin-top: 32px;
  padding: 18px 16px 0;
}
.main__cart__items__item {
  display: flex;
}
.item-detail {
  flex: 1;
  margin: 0 20px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.numbers {
  display: flex;
  margin-bottom: 17px;
}
.item-detail__numbers__minus,
.item-detail__numbers__plus {
  -webkit-appearance: none;
  border: none;
  border-radius: 50%;
  width: 26px;
  height: 27px;
  background-color: #f0f0f5;
}
.item-detail__numbers__number {
  margin: 3px 32px;
}
.item-name {
  margin-bottom: 18px;
}
.item-price {
  font-weight: bold;
}
.main__cart-title-text {
  margin: 14px 0 32px;
  font-size: 18px;
}
.main__cart__items__item {
  margin-bottom: 18px;
}
.main__cart__delivery,
.main__cart__total {
  height: 52px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid #f0f0f5;
}
</style>