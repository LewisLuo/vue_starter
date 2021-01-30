<template>
  <div class="home">
    <!-- TODO -->
    <v-container>
      <!-- Render cards -->
      <v-row>
        <v-col v-for="item in list" :key="item.name" col="12" sm="4">
          <v-card class="mx-auto" max-width="344" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4">
                  {{ item.name }}
                </div>
                <v-list-item-title class="headline mb-1">Headline 5</v-list-item-title>
                <v-list-item-subtitle>
                  Greyhound divisely hello coldly fonwderfully
                </v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-avatar tile size="80" color="grey"></v-list-item-avatar>
            </v-list-item>
            <v-card-actions>
              <v-btn outlined rounded text>Button</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import Vue from 'vue';

import extensions from '@/mixins/extensions';

export default Vue.extend({
  name: 'Home',
  mixins: [extensions],
  data: () => ({
    list: [
      { name: 'one' },
      { name: 'two' },
      { name: 'three' },
      { name: 'four' },
      { name: 'five' },
      { name: 'six' },
    ],
  }),
});
</script>
