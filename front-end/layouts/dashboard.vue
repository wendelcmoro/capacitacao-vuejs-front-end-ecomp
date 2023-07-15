<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app clipped>
      <v-list>
        <v-list-item
          v-for="page in pages"
          :key="page"
          :to="page.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ page.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="page.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar id="nav" app clipped-left dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Dashboard</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <nuxt />
    </v-content>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    pages: [
      {
        to: '/dashboard/servicos',
        title: 'Serviços',
        icon: 'mdi-format-list-text'
      },
      {
        to: '/dashboard/imagens',
        title: 'Imagens',
        icon: 'mdi-image-edit'
      },
      {
        to: '/dashboard/portifolios',
        title: 'Portifólios',
        icon: 'mdi-book-variant-multiple'
      },
      {
        to: '/dashboard/equipes',
        title: 'Equipes',
        icon: 'mdi-head-lightbulb-outline'
      },
      {
        to: '/dashboard/contatos',
        title: 'Contatos',
        icon: 'mdi-contacts'
      },
      {
        to: '/dashboard/categorias',
        title: 'Categorias',
        icon: 'mdi-select-group'
      },
      {
        to: '/dashboard/mensagens',
        title: 'Mensagens',
        icon: 'mdi-email-box'
      }
    ]
  })
}
</script>
<style>
#nav {
  background-color: #2d6760
}
</style>
