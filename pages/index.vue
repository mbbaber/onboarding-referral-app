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
        <el-button v-clipboard="() => form.token"></el-button>
        <el-button>
          Copy Code
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
import Logo from '~/components/Logo.vue'

export default {
  data() {
    return {
      form: {}, 
      text: "one free month",
    };
  },
  methods: {
    print: function (event) {
      console.log('Done');
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
