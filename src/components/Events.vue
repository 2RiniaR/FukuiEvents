<template>
  <div class="events">
    <v-container>
      <v-flex xs12 md5 offset-md7>
        <v-text-field
          v-model="search"
          append-icon="search"
          label="検索"
          single-line
          hide-details
          class="my-4"
        />
      </v-flex>
      <v-expansion-panel>
        <v-expansion-panel-content>
          <template v-slot:header>
            <h2 class="title">カテゴリで絞り込む</h2>
          </template>
          <v-layout row wrap class="pa-2">
            <div v-for="tag in tags" :key="`tag-chip-${tag}`">
              <v-btn
                round
                :color="selectTag === tag ? '#90caf9' : 'grey'"
                @click="changeSelectTag(tag)"
              >
                {{ tag }}
              </v-btn>
            </div>
          </v-layout>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-container>

    <v-container grid-list-xl>
      <v-data-iterator
        :items="events"
        :rows-per-page-items="rowsPerPageItems"
        content-class="layout row wrap"
        :search="search"
        :custom-filter="eventFilter"
      >
        <template v-slot:item="props">
          <v-flex xs12 md6>
            <EventCard :data="props.item" />
          </v-flex>
        </template>
      </v-data-iterator>
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
import EventCard from './EventCard'

const dataURL = 'https://raw.githubusercontent.com/jigjp/intern_exam/master/fukui_event.json'

export default {

  components: {
    EventCard
  },

  data() {
    return {
      rowsPerPageItems: [10, 30, {"text":"$vuetify.dataIterator.rowsPerPageAll","value":-1}],
      events: [],
      search: '',
      tags: [],
      selectTag: ''
    }
  },

  created() {
    const self = this
    axios.get(dataURL).then(res => {
      self.events = res.data
      this.tags = this.events.map((d) => [d.category])
        .reduce((a, b) => a.concat(b))
        .filter((x, i, self) => self.indexOf(x) === i)
    })
  },

  methods: {
    eventFilter(items, search) {
      const filter = (val, search) => {
        return (
          val != null &&
          typeof val !== 'boolean' &&
          (val.event_name.toString() + val.description.toString() + val.remarks.toString())
            .toLowerCase().indexOf(search) !== -1
        )
      }
      if (this.selectTag === '') return items.filter(v => filter(v, search))
      return items.filter(v => v.category === this.selectTag & filter(v, search))
    },

    changeSelectTag(tag) {
      this.selectTag = (this.selectTag === tag) ? '' : tag
    }
  }

}
</script>

<style>

</style>
