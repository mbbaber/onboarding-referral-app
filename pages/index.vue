<template>
  <div class="container">
    <div class="column-1">
      <img src="" alt="user-photo">
    </div>
    <div class="column-2">
      <p style="font-weight:bold">Name</p>
      <p>Don't forget that for each new subscriber you refer, both you and them get <b> {{ text }} </b> of coverage! 💙  </p>
      <p>Share your <b> {{ text }} </b> referral code</p>
      <div class="buttons">
        <el-form ref="form" :model="form" label-width="120px">
            <el-input v-model="form.token"></el-input>
        </el-form>
        <el-button 
          v-clipboard:copy="form.token"
          v-clipboard:success="onCopy"
          v-clipboard:error="onError"
        >Copy!
        </el-button>
        <el-button>
          <a
          href="tweet"
          target="_blank"
          class="button--blue"
        >
          Tweet
        </a>
        </el-button>
        
        <a
          href="www.facebook.com"
          target="_blank"
          class="button--blue"
        >
          Share
        </a>
      </div>
      <div>
        <p>You can also send <b> {{ text }} </b> via email, separate emails with semi-colon « ; » </p>
        <form action="">
          Another form
        </form>
      </div>
      <div>
        <el-button>Send email</el-button>
        <el-button v-on:click="print">Done</el-button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      form: {
        token: "SHARETHELOVE+5WMXM",
      }, 
      text: "one free month",
    };
  },
  methods: {
    print: function (event) {
      console.log('Done');
    },
    onCopy: function (e) {
      alert('You just copied: ' + e.text)
    },
    onError: function (e) {
      alert('Failed to copy text')
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  align-items: stretch;
}

.column-1 {
  flex: 0 1 10%;
}

.column-2 {
  flex: 0 1 90%;
}

</style>
