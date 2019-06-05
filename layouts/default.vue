<template>
  <v-app>
    <v-content>
      <v-container fluid fill-height>
        <v-layout row wrap align-center>
          <v-flex xs12 sm12 md6 lg6 offset-md3 offset-lg3>
            <v-breadcrumbs :items="items">
              <template v-slot:item="props">
                <v-breadcrumbs-item
                  :to="props.item.destination"
                  :class="[props.item.disabled && 'disabled']"
                >{{ props.item.title.toUpperCase() }}</v-breadcrumbs-item>
              </template>
            </v-breadcrumbs>
            <nuxt/>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: "Comentários",
          destination: "/"
        },
        {
          title: "Meus Comentários",
          destination: "/meus-comentarios"
        }
      ]
    };
  },
  head: {
    meta: [
      { name: 'twitter:card', content: 'summary' },
      { name: 'twitter:site', content: '@localhost' },
      { name: 'twitter:title', content: 'Simulação do Twitter' },
      { name: 'twitter:description', content: 'Esse projeto tem como intuito simular o twitter a fim de aprender mais sobre Vue.js, Nuxt.js e Flask' },
      { name: 'twitter:image', content: './assets/bird.png' },
      { name: 'twitter:image:alt', content: 'Tuiter logo' }
    ]
  }
};
</script>
