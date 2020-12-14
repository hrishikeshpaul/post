<template>
<div>
  <Navbar />
  <hr width='75%'/>
  <div class='container'>
    <div class='center'>
      <input placeholder="Type your sentence..." id='input_box' v-model='sentence' v-if='!sentence_detected'/>
      <div v-if='sentence_detected'>
        <span
          v-for='(word, idx) in sentence_array'
          :key='word' :id="word+idx"
          class='pos_words'
          >
          <span class='word_hover' @click='showWordInfo(word)'>{{word}}</span>
          <hr style='margin-top: 10px; margin-bottom: 10px;'/>
          <span
            class='pos_class'
            style='display: table-row; font-size: 18px; border: 2px solid black !important; border-radius: 5px !important; color: black !important; cursor: auto !important;'
            :id='"no_dec"+idx'
            >{{pos_abb_dict[pos_array[idx]]}}
          </span>
        </span>
      </div>
      <br />
      <button class='detect_button' @click.prevent='tryAgain' v-if='sentence_detected'>{{button_text}}</button>
      <button class='detect_button' @click.prevent='detect' :disabled='!detect_button' v-if='!sentence_detected'>{{button_text}}</button>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'

import Navbar from './NavBar'

export default {
  name: 'Home',
  components: {
    Navbar
  },
  data () {
    return {
      sentence: '',
      detect_button: false,
      sentence_detected: false,
      button_text: 'Get typing!',
      sentence_array: [],
      pos_array: [],
      pos_abb_dict: {
        'adj': 'adjective',
        'adv': 'adverb',
        'adp': 'adposition',
        'conj': 'conjunction',
        'det': 'determiner',
        'noun': 'noun',
        'num': 'numeral',
        'pron': 'proper noun',
        'prt':'particle',
        'verb':'verb'
      },
      wordInfo: 'Word info is loading...'
    }
  },
  props: {},
  watch: {
    sentence(newVal) {
      if (newVal.length > 0) {
        this.detect_button = true
        this.button_text = 'Tag the sentence!'
      } else {
        this.detect_button = false
        this.button_text = 'Get typing!'
      }
    },
    sentence_detected (newVal) {
      if (newVal === true) {
        this.button_text = 'Try again!'
      }
    }
  },
  methods: {
    tryAgain() {
      // eslint-disable-next-line no-console
      console.log('here')
      this.button_text = 'Get typing!'
      this.detect_button = false
      this.sentence = ''
      this.sentence_detected = false
    },
    showWordInfo(word) {
      let headers = {
        headers: {
          "x-rapidapi-host": "wordsapiv1.p.rapidapi.com",
          "x-rapidapi-key": "02307dd73amsh0aa96c1107234e4p1b150bjsn6adcb4a57871"
        }
      }

      this.wordInfo = 'Word info is loading...'

      axios.get(`https://wordsapiv1.p.mashape.com/words/${word}`, headers)
        .then(res => {
          // eslint-disable-next-line no-console
          console.log(res)
          this.wordInfo = res
          this.$swal({
            title: word,
            confirmButtonColor: "#FFC0CB",
            html: `<hr /><b>Frequency: </b>${res.data.frequency} <br /> <br /> <b>Part Of Speech: </b>${res.data.results[0].partOfSpeech} <br />`
          })
        })

    },
    detect() {
      this.sentence_array = this.sentence.split(' ')
      this.button_text = 'Tagging...'

      axios.post('https://post-tagger.herokuapp.com/',{sentence: this.sentence})
      .then(res => {

        // let inp = document.getElementById('input_box')
        // inp.classList.add('input_white_border')
        this.sentence_detected = true
        this.pos_array = res.data.Complex
      })
      .catch(err => {
        // eslint-disable-next-line no-console
        console.log(err)

      })
    }
  }
}
</script>

<style scoped>
.center {
  width: 100%;
  height: 100px;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: auto;
  margin-top: auto;
}


.detect_button {
  margin-top: 20px;
  border-radius: 10px;
  border: 2px solid black;
  height: 50px;
  width: 200px;
  outline: none;
  font-size: 20px;
  background-color: white;
}

.detect_button:hover {
  background-color: black;
  color: white;
  transition: all 0.5s;
}

#input_box {
  width: 70%;
  border: none;
  outline: none;
  border-bottom: 2px solid black;
  font-size: 65px;
  transition: all 2.5;
}

.input_white_border {
  border-bottom: none !important;
  transition: all 2.5;
}

::-webkit-input-placeholder {
  color: grey;
}

.word_hover:hover {
  color: pink;
  cursor: pointer;
  transition: all 0.2s ease-out;
}

.pos_words {
  padding-right: 30px;
  font-size: 65px;
  display: inline-table;
  text-align: center;
}

.pos_class {
  display: table-row;
  font-size: 17px;
  border-radius: 5px !important;
  color: black !important;
  cursor: auto !important;
}

@media only screen and (max-width: 800px) {
  #input_box {
    width: 70%;
    border: none;
    outline: none;
    border-bottom: 2px solid black;
    font-size: 35px;
    transition: all 2.5;
  }

  .pos_words {
    padding-right: 20px;
    font-size: 30px;
    display: inline-table;
    text-align: center;
  }

  .pos_class {
    display: table-row;
    font-size: 15px;
    border-radius: 5px !important;
    color: black !important;
    cursor: auto !important;
  }

  .center {
    width: 100%;
    height: 100px;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: auto;
    margin-top: 200px;
  }

}

</style>
