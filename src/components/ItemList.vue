<template>
<div>
  <q-item class="q-my-sm" clickable v-ripple @click="articleClicked()">
        <q-item-section>
            <q-item-label class="txt-of" style="font-size:1.1rem">{{ article.title }}</q-item-label>
            <q-item-label caption lines="1">{{ new Date(article.pubDate).toDateString() }}</q-item-label>
        </q-item-section>
   </q-item>
   <q-separator inset />
</div>
</template>

<script>
export default {
  name: 'ItemList',
  props: ['article'],
  methods: {
      articleClicked () {
          this.$emit('changeArticle',this.article)
      }
  } 
}
</script>

<style scoped>
    .txt-of{
        white-space: nowrap; 
        width: 100%; 
        overflow: hidden;
        text-overflow: ellipsis; 
    }
</style>
