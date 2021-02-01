<template>
  <div class="home">
    <!-- TODO -->
    <v-container>
      <!-- Render page -->
      <!-- Display switch -->
      <div class="icon-select d-flex justify-end pr-2 py-4">
        <v-btn class="mr-2" @click="displayMode = 'card'" fab>
          <v-icon>mdi-checkerboard</v-icon>
        </v-btn>
        <v-btn @click="displayMode = 'list'" fab>
          <v-icon>mdi-format-list-bulleted</v-icon>
        </v-btn>
      </div>
      <v-divider class="py-4"></v-divider>
      <!-- Display card-mode -->
      <div class="display-card" v-if="displayMode === 'card'">
        <v-row>
          <v-col v-for="item in showItems" :key="item.name" col="12" sm="4">
            <v-hover v-slot="{ hover }">
              <v-card class="mx-auto" max-width="344" outlined>
                <v-list-item v-if="hover" class="show-on-hover" three-line>
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1">{{ item.title }}</v-list-item-title>
                    <v-list-item-subtitle>{{ item.personality }}</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item v-if="!hover" class="show-default" three-line>
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1">{{ item.title }}</v-list-item-title>
                    <v-list-item-subtitle>{{ item.personality }}</v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-avatar size="100" rounded>
                    <v-img :src="item.img"></v-img>
                  </v-list-item-avatar>
                </v-list-item>
                <v-card-actions>
                  <v-btn color="pink" outlined rounded>Petting</v-btn>
                </v-card-actions>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
      </div>
      <!-- Display list-mode -->
      <div class="display-list" v-if="displayMode === 'list'">
        <v-list three-line>
          <template v-for="item in showItems">
            <v-list-item :key="item.title">
              <v-list-item-avatar><v-img :src="item.img"></v-img></v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
                <v-list-item-subtitle>{{ item.personality }}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </template>
        </v-list>
      </div>
      <!-- Pagination -->
      <v-pagination
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
  }),
  computed: {
    showItems() {
      const startIndex = this.itemsPerPage * (this.currentPage - 1);
      const shownCards = this.itemList.slice(startIndex, startIndex + this.itemsPerPage);
      return shownCards;
    },
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    },
  },
});
</script>
