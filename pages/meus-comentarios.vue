<template>
  <v-card class="card">
    <v-toolbar color="white">
      <v-toolbar-title>
        <h5 class="headline font-weight-bold tw-title">Meus comentários</h5>
      </v-toolbar-title>
    </v-toolbar>
    <v-card-text class="px-4 pb-4 v-card-comentarios">
      <v-layout row wrap class="pb-4" v-for="comentario in comments" :key="comentario.id">
        <v-flex xs12 sm12 md2 lg2>
          <v-img
            src="https://picsum.photos/500/300?image=40"
            class="grey lighten-2"
            width="72"
            height="72"
          ></v-img>
        </v-flex>
        <v-flex xs12 sm12 md10 lg10>
          <div>
            <div class="tw-nickname-comentario align-center">
              <div class="subheading font-weight-bold tw-username pb-1 pr-2">Username lastname</div>
              <div class="body-1 tw-info pb-1 pr-2">@Username</div>
              <div class="body-1 tw-info pb-1 pr-2">•</div>
              <div class="body-1 tw-info pb-1">21 de mai de 2017</div>
            </div>
            <div class="text-xs-right">
              <v-btn
                flat
                icon
                small
                color="#657786"
                class="ma-0"
                @click.stop="abrir_modal(comentario.id)"
              >
                <v-icon>keyboard_arrow_down</v-icon>
              </v-btn>
            </div>
          </div>
          <div class="body-1 tw-comment">{{ comentario.description }}</div>
        </v-flex>
      </v-layout>
      <v-dialog v-model="dialog" max-width="590">
        <v-card>
          <v-card-title>
            <div class="title-dialog font-weight-bold tw-title">Tem certeza de que deseja excluir o Tweet?</div>
            <v-spacer></v-spacer>
            <v-btn flat icon small color="#66757f" class="ma-0" @click="dialog = false">
              <v-icon>close</v-icon>
            </v-btn>
          </v-card-title>
          <v-divider></v-divider>
          <v-card-text class="body-1 tw-info pa-3">Ao confirmar, você excluirá o tweet.</v-card-text>
          <v-divider></v-divider>
          <v-card-actions class="action-dialog">
            <v-spacer></v-spacer>
            <v-btn color="#66757f" round outline class="btn-dialog" @click="dialog = false">Cancelar</v-btn>
            <v-btn color="#e0245e" round depressed dark class="btn-dialog" @click="excluir">Excluir</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-card-text>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    dialog: false,
    comments: null,
    comment_delete: null
  }),
  methods: {
    excluir() {
      axios
        .delete("http://127.0.0.1:5000/comment/" + this.comment_delete)
        .then(response => {
          this.comments.splice(this.comments.indexOf(this.comment_delete), 1);
          this.dialog = false;
        });
    },
    abrir_modal(comentario) {
      this.comment_delete = comentario;
      this.dialog = true;
    }
  },
  mounted() {
    axios
      .get("http://127.0.0.1:5000/comments")
      .then(response => (this.comments = response.data));
  },
  head: {
    title: "Página Meus Comentários",
    meta: [
      {
        hid: "description",
        name: "description",
        content:
          "A página meus comentário tem como intuito apresentar os comentários feitos na página home."
      }
    ]
  }
};
</script>

<style>
.action-dialog {
  padding: 12px;
}

.title-dialog {
  font-size: 18px;
}

.tw-title,
.tw-username,
.tw-comment {
  color: #383838;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.tw-info {
  color: #87898b;
}

.tw-comment {
  color: #14171a;
}

.tw-nickname-comentario {
  display: inline-flex;
  float: left;
}

.v-toolbar__title {
  width: 100%;
  text-align: center;
}

.v-toolbar,
.v-card,
.v-dialog,
.v-text-field.v-text-field--solo:not(.v-text-field--solo-flat)
  > .v-input__control
  > .v-input__slot {
  box-shadow: none;
}

.v-toolbar {
  border-bottom: 1px solid #bfdae5 !important;
  border-radius: 5px 5px 0 0 !important;
}

.v-card {
  border: 1px solid #bfdae5 !important;
}

.v-card,
.v-image {
  border-radius: 5px !important;
}

.v-card-comentarios {
  background-color: #fff;
}

.btn-dialog {
  text-transform: none;
  font-weight: bold;
}
</style>
