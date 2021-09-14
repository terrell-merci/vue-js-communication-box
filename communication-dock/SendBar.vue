<template>
  <div class="send-bar">
    <div class="box">
      <form>
        <textarea v-model="value" :maxlength="charLimit" :class="{ sending }" />
        <div>
          <div>
            <ronnie-button
              v-on:click="(obj) => send(obj)"
              :button="buttonObject"
              :loading="sending"
            />
          </div>
          <div :class="{ danger: atMax }">
            <span :class="{ warning: nearMax }">{{ count }}</span
            >&nbsp;/ {{ charLimit }}
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script scoped>
export default {
  data() {
    return {
      value: "",
      sendable: false,
      buttonObject: {
        icon: "send",
        size: "2rem",
        disabled: true,
        disabledIcon: "cancel_schedule_send",
        colorOnHover: "#7065bb",
      },
      charSoftLimit: 135,
      charLimit: 153,
      sending: false,
      nearMax: false,
      atMax: false,
    };
  },
  computed: {
    count() {
      return this.value.length;
    },
    canSend() {
      return this.count > 0;
    },
  },
  watch: {
    value: function (string) {
      this.nearMax = false;
      this.atMax = false;
      if (string.length == this.charLimit) {
        this.atMax = true;
      } else if (string.length > this.charSoftLimit) {
        this.nearMax = true;
      }
      if (string.length > 0) {
        this.buttonObject.disabled = false;
        return;
      }
      this.buttonObject.disabled = true;
    },
  },
  methods: {
    async send() {
      this.sending = true;
      try {
        const response = await this.post({
          message: value,
        });
        this.$parent.active_period_messages.push({
          message: value,
        });
      } catch (e) {
        console.error(e);
      } finally {
        this.sending = false;
      }
      console.log("sending...");
    },
    post(data) {
      return new Promise((resolve, reject) => {
        axios
          .post("/api/trip", data, this.$store.getters["config/GET"])
          .then((response) => resolve(response.data))
          .catch((error) => reject(error.response.status));
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
div.send-bar {
  padding: 0.5rem;

  .warning {
    color: orange;
  }

  .danger,
  .danger span {
    color: red !important;
  }

  > div.box {
    width: 100%;
    height: 100%;
    background-color: white;
    border-radius: 5px;
    border: bootstrap.$border-standard;
    padding: 1rem;

    form {
      @include bootstrap.mixin-align-left;
      width: 100%;
      height: 100%;

      textarea,
      textarea:focus {
        border: none;
      }

      textarea {
        color: bootstrap.$color;
        width: 80%;
        height: 100%;
        font-size: 0.85rem;
        font-family: inherit !important;
        outline: 0;
        resize: none !important;
        scrollbar-width: thin;

        &::-webkit-scrollbar {
          width: 2px;
        }

        &::-webkit-scrollbar-thumb {
          border-radius: 20px;
          border: 1px solid bootstrap.$color;
        }
      }

      div {
        height: 100%;
        width: 20%;

        div:nth-child(1) {
          width: 100%;
          height: 60%;
          @include bootstrap.mixin-align-center;
        }
        div:nth-child(2) {
          width: 100%;
          height: 40%;
          font-size: 0.8rem;
          @include bootstrap.mixin-align-top;
        }
      }
    }
  }
}
</style>