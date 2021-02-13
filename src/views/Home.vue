<template>
  <div class="home">
    <!-- TODO -->
    <v-container>
      <!-- Render page -->
      <v-container class="icon-select d-flex justify-space-between pr-2 py-4">
        <div class="title"><h1>20 Popular Dog Breeds</h1></div>
        <!-- Display switch -->
        <div>
          <v-btn class="mr-2" @click="displayMode = 'card'" fab>
            <v-icon>mdi-checkerboard</v-icon>
          </v-btn>
          <v-btn @click="displayMode = 'list'" fab>
            <v-icon>mdi-format-list-bulleted</v-icon>
          </v-btn>
        </div>
      </v-container>
      <!-- Search function -->
      <div class="search-bar md-2" max-width="50%">
        <v-text-field
          ref="search"
          v-model="search"
          hide-details
          label="輸入品種名"
          single-line
        ></v-text-field>
      </div>
      <v-divider class="pb-4"></v-divider>
      <!-- Display card-mode -->
      <v-container class="display-card" v-if="displayMode === 'card'">
        <v-row>
          <v-col v-for="item in showItems" :key="item.name" col="12" sm="4">
            <v-hover v-slot="{ hover }">
              <v-card class="mx-auto" max-width="500" height="160" outlined>
                <v-list-item three-line>
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1">{{ item.title }}</v-list-item-title>
                    <v-list-item-subtitle v-if="!hover" class="show-default">
                      {{ item.personality }}
                    </v-list-item-subtitle>
                    <v-list-item-subtitle v-if="hover" class="show-on-hover">
                      <p class="d-flex pt-1 text-wrap">
                        {{ item.risk }}
                      </p>
                    </v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-avatar size="100" rounded>
                    <v-img :src="item.img" />
                  </v-list-item-avatar>
                </v-list-item>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </v-container>
      <!-- Display list-mode -->
      <v-container class="display-list d-flex justify-center" v-if="displayMode === 'list'">
        <v-list max-width="800" three-line>
          <template v-for="item in showItems">
            <v-container class="d-flex justify-space-between" :key="item.title">
              <v-list-item :key="item.title">
                <v-list-item-avatar><v-img :src="item.img"></v-img></v-list-item-avatar>
                <v-list-item-content>
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                  <v-list-item-subtitle>{{ item.personality }}</v-list-item-subtitle>
                </v-list-item-content>
              </v-list-item>
              <div class="align-self-center">
                <v-dialog v-model="itemDialogOpen" width="500" :retain-focus="false">
                  <template #activator="{ on, attrs }">
                    <v-btn color="green" dark v-bind="attrs" v-on="on">More</v-btn>
                  </template>
                  <v-card outlined>
                    <v-card-title class="headline grey lighten-2">Health risk:</v-card-title>
                    <v-card-text class="mt-3">{{ item.risk }}</v-card-text>
                    <v-divider />
                    <v-card-actions>
                      <v-spacer />
                      <v-btn color="red lighten-2" dark @click="itemDialogOpen = false">
                        Close
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </div>
            </v-container>
          </template>
        </v-list>
      </v-container>
      <!-- Pagination -->
      <v-pagination
        class="pt-2"
        v-if="itemList.length > itemsPerPage"
        v-model="page"
        :length="Math.ceil(itemList.length / itemsPerPage)"
        :total-visible="5"
        @input="changePage"
        circle
      ></v-pagination>
    </v-container>
  </div>
</template>

<script>
import Vue from 'vue';

import extensions from '@/mixins/extensions';
import dataBase from '@/assets/data';

export default Vue.extend({
  name: 'Home',
  mixins: [extensions],
  data: () => ({
    itemList: dataBase,
    currentPage: 1,
    itemsPerPage: 6,
    displayMode: 'card',
    itemDialogOpen: false,
    search: '',
  }),
  computed: {
    showItems() {
      const startIndex = this.itemsPerPage * (this.currentPage - 1);
      const shownCards = this.itemList.slice(startIndex, startIndex + this.itemsPerPage);
      const searchInput = this.search.toLowerCase();
      if (!searchInput) return shownCards;
      return this.itemList.filter((item) => item.title.toLowerCase().indexOf(searchInput) > -1);
    },
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    },
    closeDialog() {
      this.itemDialogOpen = false;
    },
  },
});
</script>
