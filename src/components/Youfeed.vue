<template>
  <section>
    <button class="btn btn-primary mb-2" @click="addFeed">Nouvelle tété</button>
    <div v-for="(feed, index) in feeds" :key="index">
      <div class="list-group-item list-group-item-success text-primary">{{feed}}
      <button class="btn btn-outline-danger" @click="removeFeed(index)"><i
        class="fa-solid fa-trash-can cursor-pointer"></i></button></div>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'Youfeed',

    data() {
      return {
        feeds: []
      }
    },
    methods:{
      setFeeds(){
       this.feeds =  JSON.parse(localStorage.getItem("feeds")) || [];
      },
      addFeed(){
        this.feeds.unshift(new Date().toLocaleTimeString([], {
    weekday:'long', month:'long', day: 'numeric'})) ;
          this.sendToLocalStorage();
      },
      sendToLocalStorage() {
                localStorage.setItem(
                    "feeds",
                    JSON.stringify(this.feeds)
                );
            },
      removeFeed(feed){
        this.feeds.splice(feed,1)
        this.sendToLocalStorage()
      },


    },
    mounted(){
      this.setFeeds()
    }
  }
</script>