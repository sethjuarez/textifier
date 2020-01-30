<template>
  <div class="hello">
    <h1>Aspect Based Sentiment Analysis Model</h1>
    <div>Enter some text!</div>
    <textarea id="doc" v-model="customText" rows="5"> </textarea> 
    <br/><button id="parseButton" v-on:click="parse">Parse</button>
    <h2>Results</h2>
    <div v-html="parsed" id="response"></div>
    <div id="notifications" v-show="processing">
        {{message}}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'CustomText',
  data: function () {
    return {
        processing: false,
        customText: 'loved the sweater but hated the pants',
        message: '',
        parsed: '',
        appSettings: ''
    }
  },
  mounted: async function () {
      let response = await axios.get('config.json')
      this.appSettings = response.data
  },
  methods: {
      parse: async function () {
        this.processing = true
        this.message = 'processing...'
        try {
            let url = this.appSettings.absaEndpoint
            let response = await axios.post(url, { text: this.customText }, {
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            this.parsed = response.data.html
            console.log(response)
            this.processing = false
        } catch(error) {
            // uh oh - log error and reset
            console.log(error)
            this.processing = false
        }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#parseButton {
    font-size: 26px;
}

#doc {
    font-size: 26px;
    width: 960px;
}

#response {
    padding: 3px;
    line-height: 90px;
    font-size: 26px;
}

#notifications {
    width:150px;
    height:30px;
    display:table-cell;
    text-align:center;
    background:rgb(172, 172, 172);
    border:1px solid #000;
    top: 10px;
    left: 10px;
    position: absolute;
    padding-top: 10px;
}

.sentence {
    color: black;
    padding: 25px 10px;
    border: solid 1px black;
}

.INTENSIFIER, .OPINION, .ASPECT {
    border-radius: 10px;
    padding: 20px 10px;
}

.INTENSIFIER:after, .OPINION:after, .ASPECT:after {
    margin-left: 10px;
    padding: 3px;
    border: solid 1px #c0c0c0;
    color: #c0c0c0;
    font-size: 14px;
    border-radius: 5px;
}

.INTENSIFIER:after{
    content: "INTENSIFIER";
}

.OPINION:after{
    content: "OPINION";
}

.ASPECT:after{
    content: "ASPECT";
}

.POS {
    background-color: rgb(0, 125, 0);
    color: white;
}

.NEG {
    background-color: rgb(0, 0, 125);
    color: white;
}
</style>
