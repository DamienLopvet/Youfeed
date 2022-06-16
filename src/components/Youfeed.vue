<template>
  <section>
    <div class="d-flex flex-row justify-content-around">
      <button class="btn btn-primary mb-2" @click="addFeedLeft">tétée gauche</button>
      <button class="btn btn-primary mb-2" @click="addFeedRight">tétée droite</button>
    </div>
    <div class="container">
      <div class="row">

         <div class="col">
          <div v-for="(feedLeft, index) in feedsLeft" :key="index">
            <div class="list-group-item list-group-item-success text-primary">{{feedLeft}}
              <button class="btn btn-outline-danger" @click="removeFeedLeft(index)"><i
                  class="fa-solid fa-trash-can cursor-pointer"></i></button>
            </div>
          </div>
        </div>
        <div class="col ">
          <div  v-for="(feedRight, index) in feedsRight" :key="index">
            <div class="list-group-item list-group-item-primary text-primary">{{feedRight}}
              <button class="btn btn-outline-danger" @click="removeFeedRight(index)"><i
                  class="fa-solid fa-trash-can cursor-pointer"></i></button>
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
        feedsRight: [],
        feedsLeft: []
      }
    },
    methods: {
      setFeeds() {
        this.feedsRight = JSON.parse(localStorage.getItem("feedsRight")) || [];
        this.feedsLeft = JSON.parse(localStorage.getItem("feedsLeft")) || [];
      },
      addFeedLeft() {
        this.feedsLeft.unshift(new Date().toLocaleTimeString([], {
          weekday: 'long', month: 'long', day: 'numeric'
        }));
        localStorage.setItem(
          "feedsLeft",
          JSON.stringify(this.feedsLeft
          )
        );
      },
      addFeedRight() {
        this.feedsRight.unshift(new Date().toLocaleTimeString([], {
          weekday: 'long', month: 'long', day: 'numeric'
        }));
        localStorage.setItem(
          "feedsRight",
          JSON.stringify(this.feedsRight
          )
        );
      },

      removeFeedLeft(feed) {
        this.feedsLeft.splice(feed, 1)
        localStorage.setItem(
          "feedsLeft",
          JSON.stringify(this.feedsLeft
          )
        );
      },
      removeFeedRight(feed) {
        this.feedsRight.splice(feed, 1)
        localStorage.setItem(
          "feedsRight",
          JSON.stringify(this.feedsLeft
          )
        );
      },


    },
    mounted() {
      this.setFeeds()
    }
  }
</script>