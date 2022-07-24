<template>
  <div>
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'

export default {
  components: {
    EventCard
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
  computed: mapState({
    events: state => state.events.events
  })
}
</script>

<style scoped>
  .prompt-box {
    position: relative;
    overflow: hidden;
    padding: 1em;
    margin-bottom: 24px;
    transform: scaleY(1);
  }
  .prompt-box > .title {
    margin: 0 0 0.5em;
  }
  .prompt-box > .title > .meta {
    margin-left: 10px;
  }
  .prompt-box > .actions {
    display: flex;
    align-items: center;
  }
  .prompt-box > button {
    margin-right: 0.5em;
  }
  .prompt-box > button:last-of-type {
    margin-right: 0;
  }
  .location {
    margin-bottom: 0;
  }
  .location > .icon {
    margin-left: 10px;
  }
  .event-header > .title {
    margin: 0;
  }
  .list-group {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .list-group > .list-item {
    padding: 1em 0;
    border-bottom: solid 1px #e5e5e5;
  }
</style>