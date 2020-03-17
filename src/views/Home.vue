<template>
  <div class="app">
    <header>
      <span class="header">COVID-19 TRACKER</span>
      <span class="live-span">
          <div class="live-dot">

          </div>
          LIVE
        </span>
    </header>

    <main>

      <Tracker/>

      <TrackerCountry/>

      <article>
        <p class="info">results are updated every 10 seconds to keep you informed</p>

        <h2>What you should know about COVID-19</h2>
        <p class="pp">Coronavirus disease 2019 (COVID-19) is an infectious disease caused by severe acute respiratory syndrome coronavirus 2 (SARS-CoV-2). The disease was first identified in 2019 in Wuhan, China, and has since spread globally, resulting in the 2019–20 coronavirus pandemic. Common symptoms include fever, cough and shortness of breath. Muscle pain, sputum production and sore throat are less common. While the majority of cases result in mild symptoms, some progress to severe pneumonia and multi-organ failure. The rate of deaths per number of diagnosed cases is estimated to be 3.4% but varies by age and other health conditions.</p>
      </article>
    </main>


    <footer>
      <span>made by</span>
      <img src="logo.png" alt="FLUE LOGO">
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </footer>

  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import Tracker from '@/components/Tracker.vue';
import TrackerCountry from '@/components/TrackerCountry.vue';

export default {
  name: 'Home',
  components: {
    Tracker,
    TrackerCountry
  },


};
</script>

<style lang="scss">
  article {
    max-width: 1000px;
    padding: 50px 10px;
    .info {
      color: #999;
    }

    h2 {
      margin-top: 25px;
      font-size: 2.5em;
      font-weight: 400;
      text-align: left;
    }

    .pp {
      text-align: left;
      font-size: 1.2em;
    }
  }

  header {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 30px 0;
    @media(max-width: 800px) {
      flex-direction: column-reverse;
    }
  }

  html {
    @media (prefers-color-scheme: dark) {
      background: black;
      * {
        color: white !important;
      }

      img {
        filter: invert(2) brightness(3);
      }
    }
  }

  .header {
    font-size: 3em;
    font-weight: 300;
    @media(max-width: 600px) {
      font-size: 2em;
    }

  }
  $live-color: #E43447;
  @keyframes pulse {
    0% {
      opacity: 0;
    }
    50% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  .live-span {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    color: $live-color;
    font-size: 16px;

    @media (prefers-color-scheme: dark) {
      color: $live-color !important;
    }

    .live-dot {
      height: 5px;
      width: 5px;
      background: $live-color;
      border-radius: 15px;
      @media (prefers-color-scheme: dark) {
        background: $live-color;
      }
      display: block;
      margin-right: 6px;
      margin-left: 10px;
      animation: pulse 1s infinite ease;
    }
  }

  main {
    display: flex;
    flex-direction: column;

    .top {
      text-align: left;
      font-size: 2em;
      margin-top: 25px;
      @media(max-width: 800px) {
        padding-left: 10px;
        font-size: 1.5em;
      }
    }

    p {
      padding: 0;
      margin: 0;
    }

    .row {
      @media(max-width: 800px) {
        flex-direction: column;
      }
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;

      .element {
        margin: 0 40px;
        @media(max-width: 800px) {
          margin: 20px 40px;
        }
        border-radius: 50px;
        .icon {
          img {
            height: 100px;
            padding: 30px;
            width: auto;
            opacity: 0.8;
            @media(max-width: 600px) {
              height: 40px;
              padding: 5px;
            }
          }
        }

        .counter {
          font-size: 3em;
          @media (prefers-color-scheme: dark) {
            color: $live-color !important;
          }
        }

        .cases {
          font-size: 18px;
          color: #999;
        }

        .stoper {
          color: $live-color;
        }
      }
    }
  }

  .switch-enter-active, .switch-leave-active {
    transition: .5s;
  }
  .switch-enter, .switch-leave-to /* .fade-leave-active below version 2.1.8 */ {
    transform: translateY(-20px);
    opacity: 0;
  }

  footer {
    padding: 18px 0;
    opacity: 0.5;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    span {
      padding: 0 10px;
    }
    img {
      vertical-align: middle;
      max-height: 16px;
      width: auto;
    }
  }
</style>
