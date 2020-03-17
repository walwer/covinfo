<template>
  <div>
    <p class="top">Global data</p>
    <div class="row">
      <div class="element" v-for="(el,key) in cases" :key="key">
        <div class="icon">
          <img :src="`/${casesIcons[key]}`" alt="">
        </div>
        <transition name="switch" appear mode="out-in">
          <p class="counter" :key="el">{{formatData(el)}}</p>
        </transition>
        <transition name="switch" appear mode="out-in">
          <p v-if="savedCases && calcDiff(savedCases[key], el)!==0" class="stoper">+ {{ formatData(calcDiff(savedCases[key], el)) }}</p>
        </transition>
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
      };
    },
    methods: {
      getData() {
        const url = 'https://coronavirus-19-api.herokuapp.com/all';
        axios.get(url)
          .then((res) => {
            this.cases = res.data;
            if (this.savedCases === null) {
              this.savedCases = this.cases;
            }
          }).catch((err) => {

        }).finally(() => {

        });
      },
      calcDiff(start, end) {
        return end - start;
      },
      formatData(value) {
        return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
      },
    },
    created() {
      this.getData();
      setInterval(() => {
        this.getData();
      }, 10000);
    },
  }
</script>
