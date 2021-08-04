<template>
  <v-container fluid>
    <v-row v-if="loading">
      <v-col cols="12">
        <v-skeleton-loader
          v-bind="attrs"
          type="card-avatar, article, actions, list-item-three-line, list-item-three-line"
        ></v-skeleton-loader>
      </v-col>
    </v-row>

    <v-row v-if="!loading" justify="center" align="center">
      <v-col cols="12" sm="10" md="8">
        <v-card class="logo d-flex justify-center">
          <v-img max-height="350" :src="data.imageUrls[0]"></v-img>
        </v-card>
        <br />
        <v-card>
          <v-card-title class="headline">
            HOLIS
          </v-card-title>
          <v-card-text>
            <h2 class="text-center pb-10">
              {{ data.name }}
            </h2>

            <h4 class="text-center pb-10">
              Un total de {{ data.price }} 0 {{ data.price + 5 }}
            </h4>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
              velit laboriosam minus explicabo, eaque amet consequuntur modi
              assumenda ullam fugiat, asperiores error? Cum nesciunt eius natus,
              praesentium vitae eligendi distinctio.
            </p>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
              velit laboriosam minus explicabo, eaque amet consequuntur modi
              assumenda ullam fugiat, asperiores error? Cum nesciunt eius natus,
              praesentium vitae eligendi distinctio.
            </p>
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime
              velit laboriosam minus explicabo, eaque amet consequuntur modi
              assumenda ullam fugiat, asperiores error? Cum nesciunt eius natus,
              praesentium vitae eligendi distinctio.
            </p>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn color="primary" nuxt to="/clients" class="my-2">
              Clientes
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
type IProduct = {
  name: string;
  price: number;
  visible: boolean;
  imageUrls?: string[];
};
import Vue from "vue";
export default Vue.extend({
  data() {
    const data: IProduct = {
      name: "",
      price: 0,
      visible: false,
      imageUrls: []
    };
    const loading: boolean = true;
    return {
      data,
      loading
    };
  },
  mounted() {
    this.getMessage();
    this.loading = false;
  },
  methods: {
    async getMessage() {
      const productTestRef = this.$fire.firestore
        .collection("products")
        .doc("test");
      const testDoc = await productTestRef.get();
      this.data = testDoc.data();
    }
  }
});
</script>
