<template>
<div class="row">
    <pre v-if="bodyResponse">{{ bodyResponse }}</pre>
    <button v-on:click="print()">click</button>
</div>
</template>

<script>
export default {
  name: 'Rss',
  data () {
      return {
          bodyResponse: null
      }
  },
  created () {
    var soap = require('soap');
    var parseString = require('xml2js').parseString;
    //1. sunrise: "4:50"
    //9. distance: 279212.92467966
    //10. price: 436948.49557884
    var url = 'http://pis.predmety.fiit.stuba.sk/pis/ws/WeatherForecast?WSDL';
    var args = {
      year:'2019',
      coord_lat: '60.170830',
      coord_lon: '24.937500'
    };//60.170830	24.937500
    var body;
    soap.createClient(url, function(err, client) {

        client.getAverageTemperature (args, function(err, result) {
          if(!result[body]){
            if(err)console.log(err)
            console.log(result);  okii
          }else
            parseString(result['body'], function (err, res) {
                console.log(res);
                body=res;
            });
        });
    });
    this.bodyResponse=body;
  },
  methods : {
    print () {
      console.log(this.bodyResponse)
    }
  }
}
</script>