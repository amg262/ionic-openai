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

      <form @submit.prevent="query">
        <input id="query-string" v-model="queryString" class="form-control m-1" placeholder="Search API" type="text">
        <div class="row">
          <select v-model="select" class="form-control">
            <option v-for="o in opts" :key="o.value" :value="o.value">{{ o.name }}</option>
          </select>
        </div>
        <button id="search-button" class="btn btn-secondary" type="submit">Search</button>
      </form>


      <ion-input>
        <ion-label position="floating">Name</ion-label>
        <ion-input type="text"></ion-input>
      </ion-input>
      <div id="container">
        <strong>Ready to create an app?</strong>
        <p>Start with Ionic <a href="https://ionicframework.com/docs/components" rel="noopener noreferrer"
                               target="_blank">UI Components</a></p>
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
    query() {

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


      const openai = new OpenAIApi(configuration);
      const response = openai.createImage({
        prompt: "A cute baby sea otter",
        n: 2,
        size: "1024x1024",
      });

      console.log(response);
      this.$emit = ('search-finished', this.searchResults);
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
