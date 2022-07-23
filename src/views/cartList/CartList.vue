<template>
  <div class="wrapper">
    <div class="title">我的全部购物车(2)</div>

    <div class="carlist">
      <div class="carlist__shop">沃尔玛</div>
      <div class="carlist__list">
        <img class="carlist__list__img" src="http://www.dell-lee.com/imgs/vue3/超市.png" />
        <div class="carlist__list__p">
          <h4 class="carlist__list__title">番茄250g/份</h4>
          <p class="carlist__list__price">
            <span class="carlist__list__single ">
              <span class="carlist__list__yen">&yen;</span>
              33.6 x 3
            </span>
            <span class="carlist__list__total ">
              <span class="carlist__list__yen">&yen;</span>
              99.9
            </span>
          </p>
        </div>
      </div>
    </div>
  </div>
  <Docker :currentIndex="1" />
</template>

<script>
import Docker from '../../components/Docker.vue'
export default {
  name: 'CartList',
  components: { Docker }
}
</script>

<style lang="scss" scoped>
.wrapper {
  overflow-y: auto;
  position: absolute;
  left: 0;
  top: 0;
  bottom: .5rem;
  right: 0;
  background: rgb(248, 248, 248);
}

.title {
  line-height: .44rem;
  background: #FFF;
  font-size: .16rem;
  color: #333333;
  text-align: center;
}

.carlist {
  position: relative;
  height: 2.2rem;
  margin: .16rem .14rem;
  background: #FFFFFF;
  border-radius: .04rem;

  &__shop {
    font-size: .16rem;
    color: #333333;

  }

  &__list {
    position: relative;
    display: flex;

    &__img {
      width: 0.46rem;
      height: 0.46rem;
      margin: .16rem;
    }

    &__tittle {
      font-size: .14rem;
      color: #333333;
    }

    &__price {
      display: flex;
      line-height: .2rem;
      font-size: .14rem;
    }

    &__single {
      color: #E93B3B;
    }

    &__total {
      position: absolute;
      color: #000000;
      right: .16rem;
    }
  }
}
</style>