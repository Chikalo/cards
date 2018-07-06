
<template>
  <div id="app" class="jumbotron">
    <h1>Hello! Nice to see you!</h1>
    <hr />
    <form @submit="addMessage">
      <div class="form-group">
        <input class="form-control"
        v-model="newMessage.title"
        maxlength="40" autofocus placeholder="Please introduce yourself :)"/>
      </div>
      <div class="form-group">
        <textarea class="form-control"
        v-model="newMessage.text"
         placeholder="Leave your message!"  rows="3"></textarea>
      </div>
      <button class="btn-primary" type="submit">Send</button>
    </form>
    <div class="card-group">
    <div class="card-block" v-for="message in messages">
      <h4 class="card-title">{{message.title}}</h4>
      <p class="card-text">{{message.text}}</p>
      <p class="card-text"><small class="text-muted"> Added on {{message.timestamp}}</small></p>
    </div>
  </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
<script>
import Firebase from 'firebase'

  let config = {
apiKey: 'AIzaSyC-SaAA32_yL7bhLTqqIHqq0t1d1SAyJMQ',
authDomain:'vuejsvladimir.firebaseapp.com',
databaseURL: 'https://vuejsvladimir.firebaseio.com',
projectId: 'vuejsvladimir',
storageBucket: 'vuejsvladimir.appspot.com',
messagingSenderId: '6636695426'
}

  let app = Firebase.initializeApp(config)
  let db = app.database();
  let messagesRef = db.ref('messages')

  export default {
    name: 'App',
    firebase: {
      messages: messagesRef
    },
    data () {
      return {
        newMessage: {
          title: '',
          text: '',
          timestamp: null
        }
      }
    },
    methods: {
      addMessage (e) {
        e.preventDefault()
        if (this.newMessage.title === '') {
          return
        }
        this.newMessage.timestamp = Date.now()
        messagesRef.push(this.newMessage)
        this.newMessage.text = ''
        this.newMessage.title = ''
        this.newMessage.timetamp = null
      }
    }
  }
  </script>
