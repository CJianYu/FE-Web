<template>
    <div class="container">
      <app-header :quoteCount="quotes.length" :maxQuote="maxQuote"></app-header>
      <app-add-quote @addQuote="newQuote"></app-add-quote>
       <app-quote-grid :quotes="quotes" @quoteDeleted="deleteQuote"></app-quote-grid>
      <div class="row">
        <div class="col-sm-12 text-center">
          <div class="alert alert-info">Info:please click the quote to delete it </div>
        </div>
      </div>
    </div>
</template>

<script>
    import QuoteGrid from './components/QuoteGrid.vue';
    import NewQuote from './components/NewQuote.vue';
    import Header from './components/Header.vue'
    export default {
        data:function () {
          return {
            quotes:[
              "this is a quote to see"
            ],
            maxQuote:10,
          }
        },
      methods:{
        newQuote:function(quote){
            if(this.quotes.length>10){
                return alert("please delete quote");
            }
            this.quotes.push(quote);
        },
        deleteQuote:function (index) {
            this.quotes.splice(index,1);
        }
      },
      components:{
        appQuoteGrid:QuoteGrid,
        appAddQuote:NewQuote,
        appHeader:Header
      }
    }
</script>

<style>
</style>
