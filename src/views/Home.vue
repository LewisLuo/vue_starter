<template>
  <div class="home">
    <!-- TODO -->
    <v-container>
      <!-- Render cards -->
      <v-row>
        <v-col v-for="item in list" :key="item.name" col="12" sm="4">
          <v-hover v-slot="{ hover }">
            <v-card class="mx-auto" max-width="344" outlined>
              <v-list-item v-if="hover" class="show-on-hover" three-line>
                <v-list-item-content>
                  <v-list-item-title class="headline mb-1">{{ item.name }}</v-list-item-title>
                  <v-list-item-subtitle>ok</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>
              <v-list-item v-if="!hover" class="show-default" three-line>
                <v-list-item-content>
                  <v-list-item-title class="headline mb-1">{{ item.name }}</v-list-item-title>
                  <v-list-item-subtitle>
                    Greyhound divisely hello coldly fonwderfully
                  </v-list-item-subtitle>
                </v-list-item-content>
                <v-list-item-avatar size="80" color="grey"></v-list-item-avatar>
              </v-list-item>
              <v-card-actions>
                <v-btn outlined rounded text>Button</v-btn>
              </v-card-actions>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
      <v-pagination v-model="page" :length="list.length/3" :total-visible="5" circle></v-pagination>
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
