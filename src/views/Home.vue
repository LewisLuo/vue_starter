<template>
  <div class="home">
    <!-- TODO -->
    <v-container>
      <!-- Render page -->
      <div class="icon-select d-flex justify-end pr-2 py-4">
        <v-btn class="mr-2" @click="displayMode = 'card'" fab>
          <v-icon>mdi-checkerboard</v-icon>
        </v-btn>
        <v-btn @click="displayMode = 'list'" fab>
          <v-icon>mdi-format-list-bulleted</v-icon>
        </v-btn>
      </div>
      <v-divider class="py-4"></v-divider>
      <div class="display-card" v-if="displayMode === 'card'">
        <v-row>
          <v-col v-for="item in showCards" :key="item.name" col="12" sm="4">
            <v-hover v-slot="{ hover }">
              <v-card class="mx-auto" max-width="344" outlined>
                <v-list-item v-if="hover" class="show-on-hover" three-line>
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1">{{ item.name }}</v-list-item-title>
                    <v-list-item-subtitle>You are hovering this card.</v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item v-if="!hover" class="show-default" three-line>
                  <v-list-item-content>
                    <v-list-item-title class="headline mb-1">{{ item.name }}</v-list-item-title>
                    <v-list-item-subtitle>This is a sample card.</v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-avatar size="80" color="grey"></v-list-item-avatar>
                </v-list-item>
                <v-card-actions>
                  <v-btn color="pink" outlined rounded>Petting</v-btn>
                </v-card-actions>
              </v-card>
            </v-hover>
          </v-col>
        </v-row>
        <v-pagination
          v-if="cardList.length > cardsPerPage"
          v-model="page"
          :length="Math.ceil(cardList.length / cardsPerPage)"
          :total-visible="5"
          @input="changePage"
          circle
        ></v-pagination>
      </div>
      <div class="display-list" v-if="displayMode === 'list'"></div>
    </v-container>
  </div>
</template>

<script>
import Vue from 'vue';

import extensions from '@/mixins/extensions';
import dataBase from '@/data';

export default Vue.extend({
  name: 'Home',
  mixins: [extensions],
  data: () => ({
    cardList: dataBase,
    currentPage: 1,
    cardsPerPage: 3,
    displayMode: 'card',
  }),
  computed: {
    showCards() {
      const startIndex = this.cardsPerPage * (this.currentPage - 1);
      const shownCards = this.cardList.slice(startIndex, startIndex + this.cardsPerPage);
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
