<template>
  <div class="details-section">
    <div class="detail-row appointment">
      <div title="Current appointment">Appointment:</div>
      <div>
        {{
          `${nextAppointment.dock.dock_title.name}, ${nextAppointment.dock.city}, ${nextAppointment.dock.state} @ ${nextAppointment.date} ${nextAppointment.time} ${nextAppointment.timezone}`
        }}
      </div>
    </div>
    <div class="detail-row periods">
      <div title="Notification periods for current appointment">
        Periods ({{ nextAppointment.notification_periods.length }}):
      </div>
      <div>
        <div></div>
      </div>
    </div>
    <div class="detail-row range">
      <div title="Date range of current notification period">Date range:</div>
      <div>{{ period.start }} - {{ period.end }}</div>
    </div>
    <div class="detail-row status">
      <div title="Status of current notification period">Status:</div>
      <div>
        Driver(s)&nbsp;<b>responded</b>&nbsp;and&nbsp;
        <span :class="`text-${period.state.name.toLowerCase()}`">{{
          period.state.name.toLowerCase()
        }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    period: {
      type: Object,
      default: () => {},
    },
    nextAppointment: {
      type: Object | null,
      default: () => {},
    },
  },
};
</script>

<style lang="scss" scoped>
@use "@sass/bootstrap";
div.details-section {
  font-size: 0.8rem;
  border-bottom: 1px solid rgb(233, 236, 241);
  background-color: #eff4fa;

  > div.detail-row {
    width: 100%;
    height: 25%;
    @include bootstrap.mixin-align-left;

    > div {
      height: 100%;
      @include bootstrap.mixin-align-left;
    }

    > div:nth-child(1) {
      width: 25%;
      padding-left: 0.5rem;
    }
    > div:nth-child(2) {
      width: 75%;
      padding-right: 0.5rem;

      > div {
        min-width: 10%;
        max-width: 100%;
        height: 35%;
        border-radius: 10rem;
        background-color: blue;
      }
    }
  }
}
</style>