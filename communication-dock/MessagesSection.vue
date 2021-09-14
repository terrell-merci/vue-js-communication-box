<template>
  <div class="messages-section">
    <message
      v-for="(message, key) in messages"
      :key="key"
      :x="key"
      :message="message"
    />
  </div>
</template>

<script scoped>
import Message from "./inc/message.vue";
export default {
  components: { Message },
  props: {
    messages: {
      type: Array | null,
      default: () => [],
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
div.messages-section {
  font-size: 0.85rem;
  padding: 1rem;
  @include bootstrap.mixin-scrollable;
  scrollbar-width: thin;

  &::-webkit-scrollbar {
    width: 2px;
  }

  &::-webkit-scrollbar-thumb {
    border-radius: 20px;
    border: 1px solid bootstrap.$very-light-color;
  }
}
</style>
