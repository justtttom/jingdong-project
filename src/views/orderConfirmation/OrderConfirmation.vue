<template>
  <div class="wrapper">
    <TopArray />
    <ProductList />
    <Order />
  </div>
</template>

<script>
import TopArray from './TopArray'
import ProductList from './ProductList'
import Order from './Order'


export default {
  name: 'OrderConfirmation',
  components: { TopArray, ProductList, Order }

}
</script>

<style lang="scss" scoped>

.wrapper {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: #eee;
  overflow-y: scroll;
}
</style>