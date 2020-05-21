<template>
  <div class="row justify-center items-center" style="height:80vh; padding: 0px 40px;">
    <q-scroll-area class="col-4 col-md-4 col-xs-12 white-box " style=" min-width:330px; ">
      
      <q-list >
        <item-list v-for="art in rssArticles" :key="art.title" 
        v-bind:article="art" v-on:changeArticle="setArticle(art)">
        </item-list>
      </q-list>    

    </q-scroll-area>
    <q-space></q-space>
    <div class="col-7 col-md-7 white-box col-xs-12">
      <article-detail v-if="actualArticle" v-bind:article="getArticleByTitle(actualArticle)"></article-detail>
      <div v-else class="row justify-center items-center" style="height:100%;">
        <q-img
            src="~assets/logo--blue.png"
            class="column"
            style="height:60%; width: 50%; opacity: 0.5;">
        </q-img>  
      </div>
    </div>
  </div>
</template>

<script>
var Feed = require('rss-to-json');
import ItemList from 'components/ItemList'
import ArticleDetail from 'components/ArticleDetail'

export default {
  components: {
    'item-list': ItemList,
    'article-detail': ArticleDetail
  },
  props: [
    'url'
  ],
  name: 'PageIndex',
  data () {
      return {
          actualArticle: null,
          rssArticles: []
      }
  },
  created () {
    console.log(this.url)
    let Parser = require('rss-parser');
    let parser = new Parser();
    const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/'
    let feed;
    (async () => {
        feed = await parser.parseURL(CORS_PROXY + this.url);
        this.rssArticles=feed.items
    })();
  },
  methods : {
      print () {
          this.rssArticles.forEach(element => {
          console.log(element)
      });
      },
      getArticleByTitle (title) {
        var nasElement;
        this.rssArticles.forEach(element => {
          if (element.title==title)
            nasElement= element;
        })
        return nasElement;
      },
      setArticle(art){
        this.actualArticle=art.title
      },
      fetchByUrl () {
        let Parser = require('rss-parser');
        let parser = new Parser();
        const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/'
        let feed;
        (async () => {
            feed = await parser.parseURL(CORS_PROXY + this.url);
            this.rssArticles=feed.items
            this.actualArticle=null
        })();
      },
      sortDesc () {
          this.rssArticles.sort(function(a,b){
            return new Date(b.pubDate) - new Date(a.pubDate);
          });
      },
      sortAsc () {
          this.rssArticles.sort(function(a,b){
            return new Date(b.pubDate) - new Date(a.pubDate);
          }).reverse();
      }
  }
}
</script>
<style  scoped>
.white-box{
  background-color:rgba(256,256,256,0.6);
  height:95%;
  padding: 15px 20px;
  border: solid 0.5px rgba(76, 87, 116, 0.1);
}
</style>
