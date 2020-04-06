<template>
  <div id="app">
    <full-page :options="options" id="fullpage" v-if="isLoaded">
            <div v-for="showerThought in showerThoughts" :key="showerThought.data.id" class="section">
              <div class="container">
                  <img src="./assets/showerThoughts.jpg" alt="shower icon" style="width:20%; border-radius: 27%;">
                  <div class="quote-symbol">“</div>
                  <div class="quote"><a target="blank" :href="showerThought.data.url">{{ showerThought.data.title }}</a></div>
                  <div class="details">
                    <div class="details-author">Author: {{ showerThought.data.auth }}</div>
                    <div class="stats">{{ showerThought.data.ups }} Upvotes | {{ showerThought.data.num_comments }} Comments</div>
                  </div>
              </div>
            </div>
        </full-page>

        <div v-else>
          <LoadingSpinner/>
        </div>
  </div>
</template>

<script>
import LoadingSpinner from './components/LoadingSpinner'

export default {

  name: 'App',
  components: {
    LoadingSpinner
  },
  created(){
    fetch('https://www.reddit.com/r/Showerthoughts.json?limit=20')
    .then(response => response.json())
    .then(data => {
      this.showerThoughts = data.data.children
      this.showerThoughts.shift()
      this.showerThoughts.shift()
      this.isLoaded = true
    })
  },
  data () {
      return {
      isLoaded:false,

      showerThoughts: [],
        options: {
          
          scrollBar: true,
          sectionsColor: [
          '#AD7CFC', 
          '#41b883', 
          '#FFC300', 
          '#0798ec',
          '#F27CFC', 
          '#AFFC7C', 
          '#fec401',
          '#1bcee6', 
          '#ee1a59', 
          '#ba5be9',
          '#81CF59 ',
          '#44F3BD',
          '#AD7CFC', 
          '#b4b8ab',
          '#41b883', 
          '#ff5f45', 
          '#0798ec',
          '#44F3BD', 
          '#FCB67C',
          '#7C7FFC']
        }
      }
    },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Sriracha&display=swap');

  #app {
    font-family: 'sans-serif';
     color: #2d3748;
  }
  body{
    margin:0;
    padding:0;
  }
  h3{
    margin:0;
  }
  .container{
  margin:auto;
  max-width:800px;
  padding:80px 16px;
  }
  .section{
  text-align:center;
  }
  .quote-symbol{
  font-size:64px;
  line-height:0;
  margin-top:50px;
  color:white;
  }
  .quote a{
  text-decoration:none;
  font-family: 'Sriracha', cursive;
  color:white;
  font-size:32px;
  line-height:1.5;
  }
  .quote a:hover{
  color:#edf2f7;
  }
  .details{
  margin-top:10px;
  }
  .details-author{
  font-family: Arial, Helvetica, sans-serif;
  letter-spacing:1px;
  }
  .stats{
  font-family: Arial, Helvetica, sans-serif;
  }

</style>
