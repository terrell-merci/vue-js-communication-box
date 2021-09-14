<template>
  <div v-if="mounted" class="communication-dock">
    <title-bar />
    <messages-section :messages="messages" />
    <send-bar />
  </div>
</template>

<script scoped>
import TitleBar from "./TitleBar";
import MessagesSection from "./MessagesSection.vue";
import SendBar from "./SendBar.vue";
export default {
  components: { TitleBar, MessagesSection, SendBar },
  watch: {
    trip: function (trip) {
      this.getMessages(trip.id);
    },
  },
  computed: {
    trip() {
      return this.$store.getters["entry/GET"];
    },
    next_appointment() {
      if (!this.trip) {
        return null;
      }
      return Merci.collect(this.trip.appointments)
        .where("active", true)
        .first();
    },
    periods() {
      return this.trip.notification_periods;
    },
    active_period() {
      if (!this.trip) {
        return false;
      }
      return this.trip.active_notification_period;
    },
    active_period_messages() {
      if (!this.active_period) {
        return false;
      }
      return this.active_period.carrier_notifications;
    },
  },
  mounted() {
    this.mounted = true;
    setInterval(() => {
      this.getMessages(this.trip.id);
    }, 30 * 1000);
  },
  data() {
    return {
      mounted: false,
      messages: [],
    };
  },
  methods: {
    async getMessages(id) {
      const response = await axios.get(
        `/api/messages?trip_id=${id}`,
        this.$store.getters["config/GET"]
      );
      this.messages = response.data;
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
div.communication-dock {
  padding: 0 0.5rem;
  position: relative;
  height: 100%;
  width: 100%;
  background-color: #f6f9fc;
  border-radius: 5px;
  border: bootstrap.$border-standard;

  ::v-deep {
    $title-bar-height: calc(#{bootstrap.$page-bar-height} - 0.2rem);
    div.title-bar {
      width: 100%;
      height: $title-bar-height;
    }

    $send-bar-height: 7rem;
    div.send-bar {
      width: 100%;
      height: $send-bar-height;
    }

    div.messages-section {
      width: 100%;
      height: calc(100% - #{$title-bar-height} - #{$send-bar-height});
    }
  }
}
</style>