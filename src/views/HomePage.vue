<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Blank</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-list>
        <ion-item>
          <ion-label position="floating">Default input</ion-label>
          <ion-input placeholder="Enter text" id="query-string" v-model="queryString" class="form-control m-1"
                     type="text"></ion-input>
        </ion-item>
      </ion-list>
      <form @submit.prevent="query">
        <!-- <input id="query-string" v-model="queryString" class="form-control m-1" placeholder="Search API" type="text"> -->
        <div class="row">

        </div>
        <ion-button id="search-button" class="btn btn-secondary" type="submit">Default</ion-button>
        <!-- <button id="search-button" class="btn btn-secondary" type="submit">Search</button> -->
      </form>


      <ion-input>
        <ion-label position="floating">Name</ion-label>
        <ion-input type="text"></ion-input>
      </ion-input>
      <div id="container" style="margin-top:80%;">
        <!-- <strong>Ready to create an app?</strong> -->

        <!-- <div id="container" style="margin-top:30%;"></div> -->
        <div id="container1" style="margin-top:10%; visibility: hidden;">

        </div>
        <div id="container2" style="margin-top:10%;"></div>
        <div id="container3" style="margin-top:10%;"></div>
        <div id="container4" style="margin-top:10%;"></div>
        <div id="container5" style="margin-top:10%;"></div>

        <!-- <p>Start with Ionic <a href="https://ionicframework.com/docs/components" rel="noopener noreferrer"
                               target="_blank">UI Components</a></p> -->
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import {IonContent, IonHeader, IonPage, IonTitle, IonToolbar} from '@ionic/vue';
import {defineComponent} from 'vue';

export default defineComponent({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  props: {
    name: String
  },
  methods: {
    doThis() {

    },
    async query() {

      const {Configuration, OpenAIApi} = require("openai");
      const configuration = new Configuration({
        apiKey: "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",
      });
      // const openai = new OpenAIApi(configuration);
      // const response = openai.createCompletion({
      //   model: "text-davinci-003",
      //   prompt: "Say this is a test",
      //   temperature: 0,
      //   max_tokens: 7,
      // });
      // console.log(response);
      let val = document.getElementById("query-string").value;

      const openai = new OpenAIApi(configuration);
      const response = await openai.createImage({
        prompt: val,
        n: 5,
        size: "512x512",
      });

      const array = response.data.data;
      //const img = response.data.data[0].url;
      console.log(response.data.data[0].url);
      let i = 0;
      array.forEach(element => {
        i = i + 1;
        const img2 = element.url;
        console.log(img2);
        let str = "<ion-card>" +
            "<ion-card-header>" +
            "<ion-card-title>Card Title</ion-card-title>" +
            "<ion-card-subtitle>Card Subtitle</ion-card-subtitle>" +
            "</ion-card-header>" +

            "<ion-card-content>" +
            "<img src='" + img2 + "' />" +
            "</ion-card-content>" +
            "</ion-card>";
        // document.getElementById("container" + i).innerHTML = "<img src='" + img2 + "' />";
        document.getElementById("container" + i).innerHTML = str;

      });
      //document.write("<img src='" + img + "' />");
      //this.$emit = ('search-finished', this.searchResults);
    }
  },
  data() {


    return {
      searchTerm: '',
      searchResults: [],
      limit: 2,


    }
  }

});

</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
