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
              <a class="navbar-brand" href="/"><img src="../assets/post_logo.svg" alt="Dispute Bills">
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
        title: 'Post',
        confirmButtonColor: "#FFC0CB",
        html:'<hr/><p>Post is a simple algorithm that was developed to tagging a word corresponding to its part of speech. The algorithm makes of a probabilisitic approach along with some randomness, together which forms the basis of an algorithm called Gibbs Sampling.</p> <p>To try it out, just type  a sentence in the input box provided below, and click on the button to tag the words!</p> <hr /> Developed  by  Hrishikesh Paul',
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
