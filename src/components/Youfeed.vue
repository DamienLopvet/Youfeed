<template>
  <section>
    <div class="d-flex flex-row justify-content-around">
      <button class="btn btn-outline-warning mb-2" @click="addFeed(e = 'left')">tétée gauche</button>
      <button class="btn btn-outline-success mb-2" @click="addFeed(e = 'right')">tétée droite</button>
    </div>
    <div class="container">
      <div class="row">

        <div class="col">
          <div v-for="(feed, index) in feeds" :key="index">
            <div class="list-group-item list-group-item-success text-primary mb-1" :class="feed.side=='left'?'left':'right'">{{feed.date}}
              <small><button class="btn btn-outline-danger " @click="removeFeed(index)">
                <i class="fa-solid fa-trash-can cursor-pointer"></i>
              </button></small>
            </div>
          </div>
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
        
        let newFeed = {
          date: new Date().toLocaleTimeString([], { weekday: 'long', month: 'long', day: 'numeric' }),
          side: e
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
  .left:before{
    content:'';
    width:50%;
    height:10%;
    background-color: #ffc107!important;
    position: absolute;
    top: 0;
    left:-1px;
    border-bottom-right-radius:30px

  }
  .right:before{
    content:'';
    width:50%;
    height:10%;
    background-color: #198754!important;
    position: absolute;
    top: 0;
    right:-1px;
    border-bottom-left-radius:30px

  }
</style>