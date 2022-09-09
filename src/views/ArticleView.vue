<template>
  <div class="about">
    <div class="article" >
        <div class="logo" v-bind:style="{'background-color': randomColor()}">
          <h4>{{getFirstLetter(articles.title)}}</h4>
        </div>
        <strong>{{articles.title}}</strong>
        <p class="margin">{{articles.body}}</p>
      <h4 class="commentaire">Commentaires :</h4>
      <div v-for="commentaire in commentaires" :key="commentaires">
        <p><strong>{{commentaire.name}}</strong></p>
        <p><a href="">{{commentaire.email}}</a></p>
        <p>{{commentaire.body}}</p>
        <hr>
      </div>
    </div>
  </div> 
</template>

<script>
  // @ is an alias to /src
  import axios from 'axios'
  
  export default {
    name: 'ArticleView',
    data (){
      return{
          articles: [],
          id : this.$route.params.id,
          commentaires: [],
          colors: ['#ffbe76', '#ff7979', '#f6e58d', '#f0932b', '#eb4d4b', '#7ed6df', '#e056fd',
                '#22a6b3', '#ffc048', '#30336b', '#130f40', '#95afc0', '#c7ecee', '#30336b', 
                '#26de81', '#20bf6b', '#a55eea', '#45aaf2', '#a5b1c2', '#0fb9b1', '#B33771',
                '#F8EFBA', '#58B19F', '#F97F51', '#B33771', '#FC427B', '#D6A2E8', '#BDC581']
      }
    },
     created(){
      this.getArticles();
      this.getCommentaires();
    },
  
    methods:{
      getArticles(){
        axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
        .then(response => {
            this.articles = response.data;
            console.log(this.articles.title);
        })
        .catch(function (error) {
          console.log(error);
        });
      },
      getCommentaires(){
        axios.get(`https://jsonplaceholder.typicode.com/posts/${this.id}/comments`)
        .then(response => {
            this.commentaires = response.data;
            console.log(this.commentaires);
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
    .article{
      margin: 15px;
      text-align: left;
    }

    .margin{
      margin-top: 30px;
    }
  
    a {
      text-decoration: none;
    }

    .commentaire{
      margin-top: 60px;
      text-decoration: underline;
    }

    .logo{
      text-align: center;
      display: inline-block;
      width: 32px; 
      height: 32px;
      border-radius: 50%;
      margin-right: 1rem;
    }

  .logo h4{
    margin-top: 0.5rem;
  }
  </style>
  
