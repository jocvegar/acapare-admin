<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card class="logo py-4 d-flex justify-center">
        <NuxtLogo />
        <VuetifyLogo />
      </v-card>
      <v-card>
        <v-card-title class="headline">
          HOLIS
        </v-card-title>
        <v-card-text>
          <p>name: {{ name }}</p>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt to="/inspire">
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script lang="ts">
export default {
  data() {
    return {
      name: ""
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
      try {
        const messageDoc = await productTestRef.get();
        const data = messageDoc.data();
        this.name = data ? data.name : "";
      } catch (e) {
        this.name = "";
      }
    }
  }
};
</script>
