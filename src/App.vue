<template>
  <div id="app">
    <div class="title-section">
      <div class="container">
        <h3>users online: {{gc.online}}</h3>
        <h3>latest banned: {{gc.latest_banned}}</h3>
        <h3>user name: {{gc.user.name}}</h3>
        <h3>user id: {{gc.user.id}}</h3>
        <h3>user expertise: {{gc.user.expertise}}</h3>
        <h3>user level: {{gc.user.level}}</h3>
        <h3>user subscription: {{gc.user.is_subscriber}}</h3>
        <h3>user patent: {{gc.user.is_subscriber}}</h3><img v-bind:src="gc.user.patent" />
        <h3>game position id : {{gc.user.game_position.id}}</h3>
        <h3>game position title : {{gc.user.game_position.title}}</h3>
        <img v-bind:src="gc.user.game_position.image" />
        <h3>featured medal id: {{gc.user.featured_medal.id}}</h3>
        <h3>featured medal title: {{gc.user.featured_medal.title}}</h3>
        <img v-bind:src="gc.user.featured_medal.image" />



      </div>
    </div>
    <main class="container">
      <div class="row">


    <div class="clearfix"></div>


	</div>

  <div class="row">
    <!-- dropzone -->


  </div>




        </main>
      </div>
</template>

<script>
import axios from 'axios';

export default {
 name: 'app',
 data () {
   return {
     online: '',
     name: '',
     user: {
       name: '',
       id: '',
       expertise : '',
       is_subscriber : '',
       patent : '',
       level : '',
       game_position: {
         id: '',
         title: '',
         image: ''
       },
       featured_medal: {
         id: '',
         title: '',
         image: ''
       }
     },

   }
 },
 mounted () {
    axios
      .get('https://api.myjson.com/bins/qedp4')
      .then(response => {
        this.gc = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}

</script>

<style>
body {
 margin: 0;
}

#app {
 font-family: 'Avenir', Helvetica, Arial, sans-serif;
 -webkit-font-smoothing: antialiased;
 -moz-osx-font-smoothing: grayscale;
 color: #2c3e50;
}

main {
 text-align: center;
 margin-top: 40px;
}

header {
 margin: 0;
 height: 56px;
 padding: 0 16px 0 24px;
 background-color: #35495E;
 color: #ffffff;
}

header span {
 display: block;
 position: relative;
 font-size: 20px;
 line-height: 1;
 letter-spacing: .02em;
 font-weight: 400;
 box-sizing: border-box;
 padding-top: 16px;
}


button {
 background: #51B767;
 color: #ffffff;
 padding: 15px;
 border-radius: 0;
 font-weight: bold;
 font-size: 15px;
 border: 0;
}

.cards {
 background: #F5F5F5;
 height:400px;
}
.cards:hover {
 transform: translateY(-0.5em);
 background: #EBEBEB;
}


.cards {
  column-count: 1;
 column-gap: 1em;
   margin-top: 70px;

}
</style>
