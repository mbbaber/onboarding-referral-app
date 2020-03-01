<template>
  <div class="container">
    <div class="column-1">
      <img src="~/assets/emma-photo.png" alt="user-photo">
    </div>
    <div class="column-2">
      <p style="font-weight:bold">Emma</p>
      <p>Don't forget that for each new subscriber you refer, both you and them get <b> {{ text }} </b> of coverage! 💙  </p>
      <p>Share your <b> {{ text }} </b> referral code</p>
      <div class="buttons">
          <el-form ref="form" :model="form">
            <el-input 
              v-model="form.token"
              :disabled=true
            >
            </el-input>
          </el-form>
          <el-button
            class="copy-button"
            v-clipboard:copy="form.token"
            v-clipboard:success="onCopy"
            v-clipboard:error="onError"
          >
            <img src="~/assets/copy-icon.svg" alt="copy">
            Copy code
          </el-button>
        
        <el-button 
          v-on:click="encodeAndTweet"
        >
          <img src="~/assets/twitter-icon.svg" alt="twitter">
          Tweet
        </el-button>
        <el-button>
          <img src="~/assets/facebook-icon.png" alt="facebook">
          Share
        </el-button>
      </div>
      <div>
        <p>You can also send <b> {{ text }} </b> via email, separate emails with semi-colon « ; » </p>
        <el-form ref="form" label-width="120px">
            <el-input
              class="email-input"
              type="textarea"
              placeholder="amelie.dupont@gmail.com ; jeanmichel@gmail.com"
              v-model="emails"
            >
            </el-input>
        </el-form>
      </div>
      <div>
        <el-button
          class="send-button"
          :disabled="!hasEmail"
        >
        <img src="~/assets/send-icon.svg" alt="send-icon">
        Send {{ addressCount }} emails</el-button>
        <el-button 
          class="done-button"
          v-on:click="print"
        >
          Done
        </el-button>
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
      emails: "",
      text: "one free month",
      tweet: "Je vous partage mon code promo qui permet de bénéficier d'un mois gratuit chez la néo-assurance Luko : ",
      result: "",
      url: "https://twitter.com/intent/tweet?text=",
      addressCount: 0,
    };
  },
  watch: {
    emails: function() {
      if (this.emails.length === 0) {
        this.addressCount = 0; 
      } else {
        const filtered = this.emails.split(';').filter((e) => e.replace(' ', "") != "");
        this.addressCount = filtered.length;
      }
    }
  },
  computed: {
    hasEmail: function () {
      return this.addressCount != 0;
    },
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
    }, 
    encodeAndTweet: function () {
      this.result = this.url + encodeURIComponent(this.tweet+this.form.token);
      window.open(this.result, "_blank");
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
  margin: 30px 30px 30px 30px;
}

.column-1 {
  flex: 0 1 10%;
  align-content: center;
}

.column-2 {
  flex: 0 1 90%;
}

p {
  margin-bottom: 15px;
}

img {
  width: 80%;
  height: auto;
}

.el-input.is-disabled .el-input__inner {
  background-color: lightblue;
  color: blue;
  width: 250px;
  display: block;
  float: left;
}

.el-button {
  background-color: blue;
  color: white;
  height: 40px;
  width: 150px;
  margin-right: 15px;
  margin-bottom: 30px;
}

.el-button span img {
  width: auto;
  height: 10px;
  margin-right: 5px;
}

.copy-button {
  float: left;
}

.el-textarea {
  width: 100%;
  margin-bottom: 15px;
}

.send-button {
  background: grey;
  color: white;
}

.done-button {
  background: lightblue;
  color: blue;
  float: right;
}

.el-input {
  display: inline;
}
</style>
