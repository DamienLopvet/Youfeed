<template>
  <section>
    <div class="d-flex flex-row justify-content-around py-3" >
      <button class="btn btn-outline-warning mb-2" @click="addFeed(e = 'left')">tétée gauche</button>
      <button class="btn btn-outline-success mb-2" @click="addFeed(e = 'right')">tétée droite</button>
    </div>

    <div class="col">
      <div v-for="(feed, index) in feeds" :key="index">
        <div class="pt-3 pb-0 list-group-item list-group-item-success text-primary mb-1 d-flex flex-row flex-wrap justify-content-between align-items-baseline"
          :class="feed.side=='left'?'left':'right'">
          <p>{{new Date(feed.date).toLocaleTimeString([], { weekday: 'long', month: 'long', day: 'numeric',hour: '2-digit', minute: '2-digit' })}}</p>
          <span v-if="feed.gap" class="text-dark shadow-sm align-self-end feed-gap mb-1">+ {{ new Date(feed.gap).toISOString().slice(11, -8) }}</span>
          <button class="btn btn-outline-danger ml-auto " @click="removeFeed(index)">
            <i class="fa-solid fa-trash-can cursor-pointer"></i>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    name: 'Youfeed',

    data() {
      return {
        feeds: [],
      }
    },
    methods: {
      setFeeds() {
        this.feeds = JSON.parse(localStorage.getItem("feeds")) || [];
      },
      addFeed(e) {
        let lastFeed =  this.feeds[0]?.date
        let feedGap =  Date.now()-  parseInt(lastFeed) 
        let newFeed = {
          date: Date.now(),
          side: e,
          gap: feedGap

        }
        this.feeds.unshift(newFeed);

        localStorage.setItem(
          "feeds",
          JSON.stringify(this.feeds
          )
        );
      },

      removeFeed(feedIndex) {
        this.feeds.splice(feedIndex, 1)
        localStorage.setItem(
          "feeds",
          JSON.stringify(this.feeds
          )
        );
      },

    },
    
    mounted() {
      this.setFeeds()
    }
  }
</script>
<style>
  .left:before {
    content: '';
    width: 50%;
    height: 10%;
    background-color: #ffc107 !important;
    position: absolute;
    top: 0;
    left: -1px;
    border-bottom-right-radius: 30px
  }

  .right:before {
    content: '';
    width: 50%;
    height: 10%;
    background-color: #198754 !important;
    position: absolute;
    top: 0;
    right: -1px;
    border-bottom-left-radius: 30px
  }
  .feed-gap{
    font-size: 9px;
    border:1px solid black;
    padding: 0 5px;
    border-top-left-radius: 5px;
    border-radius: 157px 55px / 168px;
    
}
</style>