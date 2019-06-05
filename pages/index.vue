<template>
  <v-card class="card">
    <v-toolbar color="white">
      <v-toolbar-title>
        <h5 class="headline font-weight-bold tw-title">Publicar um novo comentário</h5>
      </v-toolbar-title>
    </v-toolbar>
    <v-card-text class="px-4 pb-0 v-card-index">
      <v-layout row wrap>
        <v-flex xs12 sm12 md3 lg3>
          <v-img
            src="https://picsum.photos/500/300?image=40"
            class="grey lighten-2"
            width="131"
            height="131"
          ></v-img>
        </v-flex>
        <v-flex xs12 sm12 md9 lg9>
          <h4 class="display-1 font-weight-bold tw-username pb-1">Username</h4>
          <div class="tw-nickname-local">
            <h6 class="title tw-nickname pb-1 pr-3">@Username</h6>
            <div class="body-1 tw-info pb-1">Florianópolis, SC</div>
          </div>
          <div class="body-1 font-italic tw-info pb-1">Desenvolvedora Front-End</div>
          <a class="body-1 tw-link pb-1">http://localhost/</a>
        </v-flex>
      </v-layout>
      <v-form class="pt-4">
        <v-textarea
          solo
          name="input-7-4"
          label="Solo textarea"
          placeholder="O que está acontecendo?"
          v-model="comment"
        ></v-textarea>
      </v-form>
    </v-card-text>
    <v-card-actions class="px-4 pb-3 pt-0 v-card-index">
      <v-spacer></v-spacer>
      <v-btn color="#1DA1F2" depressed round dark large class="px-4 btn-comment" @click="comentar">Comentar</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import axios from 'axios'
export default {
  data: () => ({
    drawer: null,
    comment: null
  }),
  methods: {
    comentar() {
      axios
        .post('http://127.0.0.1:5000/comment', {description: this.comment})
        .then(response => (this.comment = null, this.$router.push({ path: '/meus-comentarios'})))
    }
  },
  head: {
    title: 'Página de Comentários',
    meta: [
      { hid: 'description', name: 'description', content: 'A página de comentário tem como intuito simular o twitte do Twitter a fim de aprender mais sobre Vue.js, Nuxt.js e Flask' }
    ]
  }
};
</script>

<style>
.tw-title,
.tw-username,
.tw-nickname {
  color: #383838;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.tw-info {
  color: #657786;
}

.tw-link {
  color: #6ea3c4;
}

.tw-nickname-local {
  display: inline-flex;
}

.v-toolbar__title {
  width: 100%;
  text-align: center;
}

.v-toolbar,
.v-card,
.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  box-shadow: none;
}

.v-toolbar {
  border-bottom: 1px solid #bfdae5 !important;
  border-radius: 5px 5px 0 0 !important;
}

.card {
  border: 1px solid #bfdae5 !important;
}

.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  border: 2px solid #bfdae5 !important;
}

.v-card,
.v-image,
.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  border-radius: 5px !important;
}

.v-card-index {
  background-color: #e8f2f6;
}

.btn-comment {
  text-transform: none !important;
  font-size: 18px;
}
</style>

