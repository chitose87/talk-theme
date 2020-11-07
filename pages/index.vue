<template lang="pug">
  div
    GlobalHeader
    p test
    .container
      div(v-for="item in fbData")
        h4(v-html="item.body")
</template>

<script lang="ts">
  import {Component, Vue} from "~/node_modules/nuxt-property-decorator";
  import * as firebase from "~/node_modules/firebase";
  import GlobalHeader from "~/components/GlobalHeader.vue";

  @Component({
    components: {GlobalHeader}
  })
  export default class Index extends Vue {
    fbData: any = {};

    mounted() {
      let process = {
        env: {
          apiKey: "AIzaSyCMQZLhoMtNacYuDbVswZvemu6ZBhbJu9I",
          authDomain: "talk-theme.firebaseapp.com",
          databaseURL: "https://talk-theme.firebaseio.com",
          projectId: "talk-theme",
          storageBucket: "talk-theme.appspot.com",
          messagingSenderId: "442693737156",
          appId: "1:762563187881:web:520aae9c9bccb8916a05b8",
          // breakPoint: "768",
          // gutter: "18"
        }
      };
      firebase.initializeApp({
        apiKey: process.env.apiKey,
        authDomain: process.env.authDomain,
        databaseURL: process.env.databaseURL,
        projectId: process.env.projectId,
        storageBucket: process.env.storageBucket,
        messagingSenderId: process.env.messagingSenderId,
      });

      //routes index
      firebase.auth().onAuthStateChanged((user) => {
        firebase.firestore().collection("topic")
          .onSnapshot((query: any) => {
            query.forEach((snap: any) => {
              let v = snap.data();
              console.log(snap.id, v);
              this.$set(this.fbData, snap.id, v);
            });
          });

        // firebase.firestore().collection("outlines")
        //   .onSnapshot(Singleton.updateOutlines);
      });
    }
  }
</script>

<style lang="scss">

</style>
