<template>
  <section class="container main">
    <div class="left-content">
      <!-- form part -->
      <Form />
    </div>
    <div class="cart">
      <!-- cart part -->
      <Cart />
      <!-- button part -->
    </div>
  </section>
</template>

<script>
import Form from "./../components/Form";
import Cart from "./../components/Cart";

export default {
  components: {
    Form,
    Cart,
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
}
</style>