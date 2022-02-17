<template>
  <section class="container main">
    <div class="left-content">
      <!-- form part -->
      <Form @free="pass" @transit="pass" />
    </div>
    <div class="cart">
      <!-- cart part -->
      <Cart :passPrice="transitPrice" />
      <!-- button part -->
    </div>
  </section>
</template>

<script>
import Form from "./../components/Form";
import Cart from "./../components/Cart";

export default {
  data() {
    return {
      transitPrice: "免費",
    };
  },
  components: {
    Form,
    Cart,
  },
  methods: {
    //傳遞運費的函式
    pass(price) {
      this.transitPrice = price;
    },
  },
};
</script>

<style scope>
.container {
  width: 90%;
  margin: 0px auto;
}
.main {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-column-gap: 30px;
}

.left-content {
  grid-column: 1 / 7;
}

.cart {
  grid-column: 7 / 13;
  margin-top: 75px;
}
</style>