<template>
  <v-app dark :style="{ background: $vuetify.theme.themes[theme].background }">
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      absolute
    >
      <v-list shaped>
        <div v-for="(item, idx) in items" :key="idx">
          <v-list-item v-if="!item.children" :to="item.to" router exact>
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title v-text="item.title" />
            </v-list-item-content>
          </v-list-item>

          <v-list-group
            v-if="item.children"
            :key="item.title"
            v-model="item.active"
            value="true"
            link
            color="info"
          >
            <template v-slot:activator>
              <v-list-item-icon v-if="item.icon">
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>

              <v-list-item-content>
                <v-list-item-title v-text="item.title"> </v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="(subItem, idx) in item.children"
              :key="`children-${idx}`"
              :to="subItem.link"
            >
              <v-list-item-icon>
                <v-icon v-text="subItem.icon"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title v-text="subItem.title"> </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
        </div>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon
        v-if="$vuetify.breakpoint.mobile"
        @click.stop="drawer = !drawer"
      ></v-app-bar-nav-icon>
      <v-btn v-else icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? "right" : "left"}` }}</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" class="ml-1" />
      <v-spacer />
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" right temporary fixed>
      <v-list>
        <v-list-item @click.native="rightDrawer = !rightDrawer">
          <v-list-item-action>
            <v-icon light>
              mdi-tshirt-crew
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Menu 2</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer absolute app>
      <span class="mx-auto">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: true,
      drawer: true,
      items: [
        {
          icon: "mdi-apps",
          title: "Inicio",
          to: "/"
        },
        {
          icon: "mdi-note-multiple",
          title: "Ordenes",
          to: "/orders"
        },
        {
          icon: "mdi-basket",
          title: "Productos",
          to: "/products",
          children: [
            {
              title: "Ver Productos",
              link: "/products/all",
              icon: "mdi-tshirt-crew"
            },
            {
              title: "Ver Categorias",
              link: "/products/categories",
              icon: "mdi-view-grid"
            }
          ]
        },
        {
          icon: "mdi-account-group",
          title: "Clientes",
          to: "/clients"
        },
        {
          icon: "mdi-cog",
          title: "Configuración",
          to: "/settings"
        }
      ],
      miniVariant: false,
      rightDrawer: false,
      title: "Acapare"
    };
  },
  computed: {
    theme() {
      return this.$vuetify.theme.dark ? "dark" : "light";
    }
  }
};
</script>
