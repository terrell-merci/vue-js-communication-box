<template>
  <div class="message" :class="`message-${message.direction}`">
    <div v-show="showDate" class="date">
      <div></div>
      <div>{{ message.date }}</div>
    </div>
    <div class="item">
      <div class="time">
        <span v-show="showTime">{{ message.time }}</span>
      </div>
      <div class="main">
        <div class="bubble">
          <span
            :title="title"
            :class="`text-${message.state.name.toLowerCase()}`"
            >{{ message.state.name }}&nbsp;&nbsp;&nbsp;</span
          >{{ message.message }}
        </div>
        <div v-show="showInfo" v-if="message.direction == 'sent'" class="info">
          <i
            class="fa fa-paper-plane-o"
            :title="`Docket SMS`"
            aria-hidden="true"
          ></i>
          &nbsp;to&nbsp;<span title="via +1 (661) 472-7032">lead driver</span>
        </div>
        <div v-show="showInfo" v-else class="info">
          from&nbsp;<span title="via +1 (661) 472-7032">lead driver</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script scoped>
export default {
  props: {
    x: {
      type: String,
      default: 0,
    },
    message: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    allMessages() {
      return this.$parent.messages;
    },
    prevMessage() {
      if (this.x == 0) {
        return null;
      }
      return this.allMessages[this.x - 1];
    },
    nextMessage() {
      if (this.x == this.allMessages.length - 1) {
        return null;
      }
      return this.allMessages[this.x + 1];
    },
    showDate() {
      if (!this.prevMessage) {
        return true;
      }
      return this.prevMessage.date !== this.message.date;
    },
    showTime() {
      if (!this.prevMessage) {
        return true;
      }
      if (this.prevMessage.from !== this.message.from) {
        return true;
      }
      return this.prevMessage.time !== this.message.time;
    },
    showInfo() {
      if (!this.nextMessage) {
        return true;
      }
      return this.nextMessage.from !== this.message.from;
    },
    readout() {
      return this.message.state.readout.replace("_", "").replace("_", "");
    },
    title() {
      if (this.message.direction == "sent") {
        return this.readout;
      }
      return `Docket has determined that the ${this.readout.toLowerCase()} in this message.`;
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
div.message {
  font-size: 0.8rem;
  height: fit-content;
  min-height: 2rem;
  width: 100%;

  > div.date {
    position: relative;
    height: 1rem;
    width: 100%;
    margin: 0.5rem 0;
    overflow: hidden;

    > div:nth-child(1) {
      position: absolute;
      top: calc(50% - 1px);
      left: 5%;
      height: 2px;
      width: 90%;
      background-color: rgba(255, 255, 255, 0);
      border: 1px solid #e3edf6;
    }

    > div:nth-child(2) {
      position: absolute;
      top: 0;
      left: 45%;
      width: 15%;
      height: 100%;
      background-color: rgb(246, 249, 252);
      @include bootstrap.mixin-align-center;
    }
  }

  > div.item {
    height: fit-content;
    width: 100%;
    padding: 0.1rem 0;
    @include bootstrap.mixin-align-top-left;

    > div {
      height: fit-content;
    }

    > div.time {
      width: 15%;
      padding: 0.5rem 0;
    }

    > div.main {
      width: 85%;

      > div.bubble {
        height: fit-content;
        width: fit-content;
        min-width: 2rem;
        max-width: 100%;
        padding: 0.5rem 1rem;
        border-top-left-radius: 20px;
        border-top-right-radius: 20px;
      }

      > div.info {
        padding: 0 1rem;
      }
    }
  }

  &.message-sent {
    div.main {
      padding-left: 4rem;
      > div.bubble {
        background-color: #d1e0f0;
        border-bottom-left-radius: 20px;
      }

      > div.info {
        @include bootstrap.mixin-align-right;
      }
    }
  }

  &.message-recd {
    div.main {
      padding-right: 4rem;
      > div.bubble {
        background-color: #ffffff;
        border-bottom-right-radius: 20px;
      }
    }
  }
}
</style>