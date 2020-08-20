<template>
  <div class="home">
  
      <div class="row m-5 px-4">
        <div class="container">
    <form class="mb-4" @submit.prevent="addMessage">
    <div class="form-group">
      <label for="username">User Name:</label>
      <input v-model="message.username" type="text" class="form-control" id="username" placeholder="Anonymous" required>
    </div>
    <div class="form-group">
      <label for="subject">Subject:</label>
      <input v-model="message.subject" type="text" class="form-control" id="subject" placeholder="Subject" required>
    </div>
    <div class="form-group">
      <label for="message">Message</label>
      <textarea v-model="message.message" class="form-control" id="message" rows="3"></textarea>
    </div>
    <div class="form-group">
      <label for="imageUrl">ImageUrl:</label>
      <input v-model="message.imageUrl" type="url" class="form-control" id="imageUrl" placeholder="Enter you image url" required>
    </div>
    <button type="submit" class="btn btn-primary">Add Message</button>
</form>
        <div class="media mb-3" v-for="message in reversedMessages" :key="message._id">
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
    message: {
      username: '',
      subject: '',
      message: '',
      imageUrl: ''
    }
  }),
  computed: {
    reversedMessages(){
      return this.messages.slice().reverse();
    }
  },
  mounted() {
    fetch(API_URL)
      .then((res) => res.json())
      .then((result) => {
        this.messages = result;
      });
  },
  methods: {
    addMessage() {
       fetch(API_URL, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(this.message),
      })
      .then(response => response.json())
      .then(data => {
        console.log('Success:', data);
      })
    }
  }
};
</script>
