<template>

    <div class="ad">
        <h2 class="txt-of ">{{ article.title }}</h2>
        <q-item-label caption lines="1" class="ad-date ">{{ new Date(article.pubDate).toLocaleString() }}</q-item-label>
        <div style="width: 100%; padding:10px;" class="column items-center">
            <q-img
                :src="article.enclosure.url"
                style="width: 75%; border-radius:2px; margin-top:10px "
                class="col">
                <div class="absolute-bottom text-subtitle1 text-center fw-li"
                    style="font-size:0.7rem; letter-spacing:0.5px;">
                    {{ article.content }}
                </div>
            </q-img>  
        </div>
        <div class="divider"></div>
        <div class="text-center">
            <a :href="article.link" class="fw-li click-link" target="_blank">Otvoriť celý článok</a>
        </div>
    </div>
   

</template>

<script>
export default {
  name: 'ArticleDetail',
  props: ['article'],
 
}
</script>

<style scoped>
    .ad{
        height:100%;
        display: flex;
        flex-direction: column;
        justify-content: stretch;
    }
    h2{
        margin:0px;
        font-size: 1.6rem;
        line-height: 1.8rem;
        letter-spacing: 0.004em;
        color:rgba(34,58,92);
    }
    .ad-date{
        padding: 5px 0px;
    }
    .click-link{
        font-size: 1.2rem;
        line-height: 1.8rem;
        letter-spacing: 0.05em;
        color:rgba(34,58,92);
        text-decoration: none;
        padding-bottom: 10px;
    }
    .divider{
        flex-grow: 1;
    }
    @media only screen and (max-width: 1023px) {
    .divider{  
      flex-grow: unset;
    }
  }
</style>
