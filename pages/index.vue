<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <br />
      <v-card>
        <v-card-title class="headline">
          HOLIS
        </v-card-title>
        <v-card-text>
          <p>name: {{ name }}</p>
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
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    const name: string = "";
    return {
      name
    };
  },
  mounted() {
    this.getMessage();
  },
  methods: {
    async getMessage() {
      const productTestRef = this.$fire.firestore
        .collection("products")
        .doc("test");
      const testDoc = await productTestRef.get();
      const data = testDoc.data();
      this.name = data ? data.name : "";
    }
  }
});
</script>
