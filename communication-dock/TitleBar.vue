<template>
  <div class="title-bar">
    <div class="title-bar__tle">
      Communication
      <ronnie-loader v-show="loading" />
    </div>
  </div>
</template>
<script scoped>
export default {
  computed: {
    loading() {
      return this.$parent.loading;
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
$padding: 0.35;
.title-bar {
  color: #8f8f8f;
  padding: 0 1rem;
  border-bottom: 1px solid rgb(233, 236, 241);
  @include bootstrap.mixin-unselectable;
  @include bootstrap.mixin-align-left;

  @include bootstrap.media-for-size(ivl) {
    height: calc(#{calc(#{bootstrap.$page-bar-height} - 0.2rem)} - 1vh);
  }

  &__tle {
    @include bootstrap.mixin-align-left;
    @include bootstrap.mixin-div-title(inherit, inherit, normal);

    > div:nth-child(1) {
      margin-left: 1rem;
      height: 2rem;
      width: 2rem;
      border-radius: 50%;
      @include bootstrap.mixin-align-center;

      > i,
      > span {
        color: #c5d9ec;
        font-size: 1.3rem;
      }
    }
  }
}
</style>