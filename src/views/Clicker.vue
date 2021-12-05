<template>
  <div class="clicker">
    <h2>Click to get Friends</h2>
    <div id="thumb" v-on:click="clickCalc()">
      <img src="../assets/thumbs-up.gif" height="229" width="239"/>
    </div>
    <br>
    <div id="clicks">Clicks: {{ numOfClicks }}
      <br>
      <span class="text">you get 1 new friend per 10 clicks</span></div>
    <br>
    <br><br>
    <div id="friends">Friends: {{ numOfFriends }}
      <br>
      <span class="text">you lose 1 friend every 5 seconds</span></div>
    <br>
    <br><br>
    <div id="maxfriends">{{ maxNumOfFriends }}<br>max Friends you ever had
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      numOfClicks: 0,
      numOfFriends: 0,
      tempClicks: 0,
      maxNumOfFriends: 0,
    }
  },
  methods: {
    clickCalc: function () {
      this.numOfClicks = this.numOfClicks + 1;
      this.tempClicks = this.tempClicks + 1;
      if (this.tempClicks == 10) {
        this.numOfFriends = this.numOfFriends + 1;
        this.tempClicks = 0;
        if (this.numOfFriends > this.maxNumOfFriends) {
          this.maxNumOfFriends = this.numOfFriends;
        }
      }
    },
    decreaseFriends: function () {
      this.numOfFriends = this.numOfFriends - 1;
      if (this.numOfFriends < 0) {
        this.numOfFriends = 0;
      }
    }
  },
  mounted() {
    setInterval(this.decreaseFriends, 5000)
  }
}


</script>

<style scoped>
#clicks, #friends, #maxfriends {
  font-size: xx-large;
}

.text {
  font-size: medium;
}
</style>