<template>
  <div class="home">
      <div class="article">
        <table class="table">
          <tr>
              <th>Titre Article</th>
              <th></th>
          </tr>
          <tr v-for="article in articles" :key="article.id">
              <td>
                <div class = "logo" v-bind:style="{'background-color': randomColor()}">
                  <p>{{getFirstLetter(article.title)}}</p>
                </div>{{article.title}}
              </td>
              <td>
                <router-link :to="{name: 'article', params: {id: article.id}}">Voir plus</router-link></td>
          </tr>
        </table>
      </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'AccueilView',
  components: {
    HelloWorld
  },
  data (){
    return{
        articles:[{id:'1', title:'aer'}],
        colors: ['#ffbe76', '#ff7979', '#f6e58d', '#f0932b', '#eb4d4b', '#7ed6df', '#e056fd',
                '#22a6b3', '#ffc048', '#30336b', '#130f40', '#95afc0', '#c7ecee', '#30336b', 
                '#26de81', '#20bf6b', '#a55eea', '#45aaf2', '#a5b1c2', '#0fb9b1', '#B33771',
                '#F8EFBA', '#58B19F', '#F97F51', '#B33771', '#FC427B', '#D6A2E8', '#BDC581']
    }
  },
   created(){
    this.getArticles();
  },

  methods:{
    getArticles(){
      axios.get("https://jsonplaceholder.typicode.com/posts")
      .then(response => {
          this.articles = response.data;
          console.log(this.articles);
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    randomColor(){
      const color = Math.floor(Math.random() * this.colors.length);
      return this.colors[color];
    },

    getFirstLetter(title){
      return title.substr(0,1).toUpperCase()
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .table{
    width: 100%;
  }
  .table{
    border-collapse: collapse;
  }
  .table td, .table th {
    border: 1px solid #ddd;
    padding: 8px;
  }

  .table tr:nth-child(even) {
    background-color: #f2f2f2;
  }

  .table tr:hover {
    background-color: #ddd;
  }

  th {
    text-align: center;
    background-color: rgb(248, 151, 106);
  }

  .article{
    margin: 15px;
  }

  a {
    text-decoration: none;
  }

  .logo{
    text-align: center;
    display: inline-block;
    width: 32px; 
    height: 32px;
    border-radius: 50%;
    margin-right: 1rem;
  }

  .logo p{
    margin-top: 0.5rem;
  }
</style>
