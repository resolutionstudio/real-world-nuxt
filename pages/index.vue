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
import EventCard from '~/components/EventCard.vue'
export default {
  head() {
    return {
      title: 'Event Listing',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            'Where you can find all the events taking place in your neighbourhood'
        }
      ]
    }
  },
  components: {
    EventCard
  },
  computed: {
    ...mapState({
      events: (state) => state.events.events
    })
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch. Please try again'
      })
    }
  }
}
</script>
