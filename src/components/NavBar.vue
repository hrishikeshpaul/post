<template>
<div>

  <div class="container">
  <nav class="navbar navbar-default">
    <div class="container-fluid">
      <div class="navbar-header">
        <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
              <a class="navbar-brand" href="/"><img src="../assets/post_logo.svg" alt="POST Logo">
      </a>
      </div>

      <div id="navbar" class="navbar-collapse collapse">
        <ul class="nav navbar-nav navbar-right" style=' vertical-align: middle;'>
          <li><a href="#" @click.prevent='showInfo'>Info</a></li>
          <li><a href="#" @click='openGithub'>GitHub</a></li>
        </ul>
      </div>
    </div>
  </nav>
</div>
</div>
</template>

<script>
export default {
  name: 'Navbar',
  methods: {
    openGithub() {
      window.location.href="https://github.com/hrishikeshpaul/pos-tagger"
    },
    showInfo(){
      this.$swal({

        width: '500px',
        confirmButtonColor: "#FFC0CB",
        html:'<p style="font-size: 30px; font-weight: 400 !important; margin-top: 10px;">Post</p><hr/><p style="font-size: 17px; font-weight: 300 !important;">Post is a simple algorithm that was developed to tagging a word corresponding to its part of speech. The algorithm makes of a probabilisitic approach along with some randomness, together which forms the basis of an algorithm called Gibbs Sampling.</p><p style="font-size: 17px; font-weight: 300 !important;">To try it out, just type  a sentence in the input box provided below, and click on the button to tag the words!</p><hr /><p style="font-size: 12px; font-weight: 300 !important;">Developed By <a href="https://www.linkedin.com/in/hrishikeshpaul/" target="_blank">Hrishikesh Paul</a></p>',
      })
    }
  }
}
</script>

<style scoped>
.navbar-brand {
  transform: translateX(-50%);
  left: 50%;
  position: absolute;
}


/* DEMO example styles for logo image */
.navbar-brand {
  padding: 0px;
}
.navbar-brand>img {
  height: 160px;
  width: 200px;
  margin-top: -7px;
  /* padding: 7px 14px; */

}

.navbar-default {
  background-color: white;
  border: none;
}

.navbar-default .navbar-collapse, .navbar-default .navbar-form {
  border: none;
}

.navbar-default .navbar-toggle {
  background-color: pink;
  border: none;
}

.navbar-default .navbar-toggle .icon-bar {
  background-color: black;
}

/deep/ .swal2-title {
  font-weight: 300 !important;
}

@media only screen and (max-width: 800px) {
  .navbar-brand {
    transform: translateX(0);
    left: 0;
    margin-top: -15px;
    margin-left: -10px;
    position: absolute;
  }

  .navbar-brand>img {
    height: 140px;
    width: 200px;
    margin-top: 10px;
    /* padding: 7px 14px; */
  }
}
</style>
