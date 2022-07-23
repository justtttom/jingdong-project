<template>
  <div class="wrapper">
    <div class="top">
      <div class="top__info">
        <div class="top__info__name">热心市民李</div>
      </div>
    </div>
  </div>
  <Docker :currentIndex="3" />
</template>

<script>
import Docker from '../../components/Docker.vue'
export default {
  name: 'My',
  components: { Docker }
}
</script>

<style lang="scss" scoped>
@import'../../style/viriables.scss';

.wrapper {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-color: #FFF;
  overflow-y: scroll;
}

.top {
  position: relative;
  height: 100%;
  background-size: 100% 2rem;
  background-image: linear-gradient(239deg, #3A6FF3 0%, #50C7FB 100%);
  background-repeat: no-repeat;

  &__info {
    position: absolute;
    top: 1.08rem;
    left: .18rem;
    right: .18rem;
    width: auto;
    height: 2.1rem;
    background: #FFFFFF;
    box-shadow: 0 .08rem .16rem 0 rgba(0, 0, 0, 0.08);
    border-radius: .08rem;

    &__name {
      font-size: .24rem;
      color: #262628;
      text-align: center;
      letter-spacing: .0019rem;
      line-height: .36rem;
    }
  }
}
</style>