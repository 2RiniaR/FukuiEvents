<template>
  <div class="event-dialog">
    <v-card class="pa-3">
      <v-chip color="green" text-color="white">{{ data.category }}</v-chip>
      <v-card-title primary-title class="title">{{ data.event_name }}</v-card-title>
      <v-divider/>
      <v-card-text>
        <p class="subheading">{{ data.description }}</p>
        <p class="body-2">{{ data.remarks }}</p>
        <v-list dense>
          <v-list-tile v-if="data.start_date && data.end_date">
            <h3 class="body-1">
              <v-icon>calendar_today</v-icon>
              {{ data.start_date }} ～ {{ data.end_date }}
            </h3>
          </v-list-tile>
          <v-list-tile v-if="data.contact">
            <h3 class="body-1">
              <v-icon>call</v-icon>
              {{ data.contact }}
              <span v-if="data.contact_phone_number">
                （{{ data.contact_phone_number }}）
              </span>
            </h3>
          </v-list-tile>
          <v-list-tile v-if="data.event_place">
            <h3 class="body-1">
              <v-icon>place</v-icon>
              <span v-if="data.event_place_url">
                <a :href="data.event_place_url">{{ data.event_place }}</a>
              </span>
              <span v-else>
                {{ data.event_place }}
              </span>
              <span v-if="data.address">
                （{{ data.address }}）
              </span>
            </h3>
          </v-list-tile>
          <v-list-tile v-if="data.mail_address">
            <h3 class="body-1">
              <v-icon>mail</v-icon>
              {{ data.mail_address }}
            </h3>
          </v-list-tile>
          <v-list-tile v-if="data.transportation">
            <h3 class="body-1">
              <v-icon>train</v-icon>
              {{ data.transportation }}
            </h3>
          </v-list-tile>
        </v-list>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
      default: () => {}
    }
  }
}
</script>

<style>

</style>
