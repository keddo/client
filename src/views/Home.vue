<template>
  <div class="home">
    <div class="container-fluid">
      <div class="row m-5">
        <div class="media mb-3" v-for="message in messages" :key="message._id">
        <img :src="message.imageUrl" class="mr-3" :alt="message.subject" width="200" height="200">
        <div class="media-body">
          <h5 class="mt-0">{{message.subject}}</h5>
          {{message.message}}
        </div>
      </div>  
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
const API_URL = 'http://localhost:1234/messages';

export default {
  name: 'Home',
  data: () => ({
    messages: [],
  }),
  mounted() {
    fetch(API_URL)
      .then((res) => res.json())
      .then((result) => {
        this.messages = result;
      });
  },
};
</script>
