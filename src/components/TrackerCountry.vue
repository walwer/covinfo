<template>
  <div v-if="display">
    <p class="top">In your country ({{country}})</p>
    <div class="row">
      <div class="element" v-for="key in displayedCases" :key="key">
        <div class="icon">
          <img :src="`/${casesIcons[key]}`" alt="">
        </div>
        <transition name="switch" appear mode="out-in">
          <p class="counter" :key="cases[key]">{{formatData(cases[key])}}</p>
        </transition>
        <transition name="switch" appear mode="out-in">
          <p v-if="savedCases && calcDiff(savedCases[key], cases[key])!==0" class="stoper">+ {{ formatData(calcDiff(savedCases[key], cases[key])) }}</p>
        </transition>
        <p>{{ cases[getTodayKey(key)] || 0 }} (today)</p>
        <p class="cases">{{key}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        country: 'Poland',
        displayedCases: ['cases', 'deaths', 'recovered'],
        casesIcons: {
          cases: 'cough.svg',
          deaths: 'death.svg',
          recovered: 'plaster.svg',
        },
        cases: {
          cases: 0,
          deaths: 0,
          recovered: 0,
        },
        savedCases: null,
        display: false
      };
    },
    methods: {
      getBrowserCountry() {
        var requestUrl = "http://ip-api.com/json";
        let country = null;
        axios.get(requestUrl)
        .then((res)=>{
          country = res.data.country;
          this.country = country;
          this.getData();
        }).catch((err)=>{

        }).finally(()=>{

        });

        return country;
      },
      getTodayKey(key){
        key = key.toString();
        key = key.split('');
        key[0] = key[0].toUpperCase();
        key = key.join('');
        key = 'today'+key;
        return key;
      },
      getData() {
        const url = 'https://coronavirus-19-api.herokuapp.com/countries';
        axios.get(url)
          .then((res) => {
            let data = res.data.filter(el=>el.country===this.country);
            if(data) {
              this.cases = data[0];
              if (this.savedCases === null) {
                this.savedCases = this.cases;
              }
              this.display = true;
            } else {
              this.display = false;
            }

          }).catch((err) => {

        }).finally(() => {

        });
      },
      calcDiff(start, end) {
        return end - start;
      },
      formatData(value) {
        if(!value) return 0;
        return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
      },
    },
    created() {
      this.getBrowserCountry();
      setInterval(() => {
        this.getData();
      }, 10000);
    },
  }
</script>
