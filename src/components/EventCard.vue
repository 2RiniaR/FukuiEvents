<template>
  <div class="event-card">
    <v-tooltip top color="blue" min-width="120" nudge-bottom="30">
      <template v-slot:activator="{ on }">
        <v-card class="pa-2" ripple elevation-3 hover v-on="on" @click="isDialogActive = true">
          <v-chip color="green" text-color="white">{{ data.category }}</v-chip>
          <v-card-title primary-title class="title">{{ data.event_name }}</v-card-title>
          <v-divider/>
          <v-card-text>{{ data.description }}</v-card-text>
        </v-card>
      </template>
      <h3 class="text-xs-center body-2">Click!!</h3>
    </v-tooltip>

    <v-dialog v-model="isDialogActive">
      <EventDialog :data="data" />
    </v-dialog>
  </div>
</template>

<script>
import EventDialog from './EventDialog'

export default {

  components: {
    EventDialog
  },

  props: {
    data: {
      type: Object,
      required: true,
      default: () => {}
    }
  },

  data() {
    return {
      isDialogActive: false
    }
  }

}
</script>

<style>

</style>
