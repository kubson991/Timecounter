<template>
  <main>
    <h1>WE'RE LAUNCHING SOON</h1>
    <section class="cloack">
      <div class="cloack__days">
        <p>{{ REMAINING_DAYS }}</p>
        <p class="back">{{ REMAINING_DAYS2 }}</p>
      </div>
      <div class="cloack__hours">
        <p>{{ REMAINING_HOURS }}</p>
        <p class="back">{{ REMAINING_HOURS2 }}</p>
      </div>
      <div class="cloack__minutes">
        <p>{{ REMAINING_MINUTES }}</p>
        <p class="back">{{ REMAINING_MINUTES2 }}</p>
      </div>
      <div class="cloack__seconds">
        <p>{{ REMAINING_SECONDS }}</p>
        <p class="back">{{ REMAINING_SECONDS2 }}</p>
      </div>
    </section>
    <section class="cloack">
      <p class="titles">DAYS</p>
      <p class="titles">HOURS</p>
      <p class="titles">MINUTES</p>
      <p class="titles">SECONDS</p>
    </section>
    <section class="social-networks">
      <a href="https://www.facebook.com/sebastian.povedaflorez"><span class="facebook"></span></a><a href="https://co.pinterest.com/poveda1999/_saved/"><span class="pinterest"></span></a><a href="https://www.instagram.com/sebastianpovedaflorez/"><span class="instagram"></span></a>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      fechaObjetivo: "",
      REMAINING_SECONDS: 0,
      REMAINING_SECONDS2: 0,
      REMAINING_MINUTES: 0,
      REMAINING_MINUTES2: 0,
      REMAINING_HOURS: 0,
      REMAINING_HOURS2: 0,
      REMAINING_DAYS: 0,
      REMAINING_DAYS2: 0,
      state: true,
      stateM: true,
      stateH: true,
      stateD: true,
    };
  },
  beforeMount() {
    const anoActual = new Date().getFullYear();
    const mesActual = new Date().getMonth();
    const diaActual = new Date().getDate();
    if (mesActual === 11 && diaActual > 25) {
      this.fechaObjetivo = new Date(`12/25/${anoActual + 1} 12:00 AM`);
    } else {
      this.fechaObjetivo = new Date(`12/25/${anoActual} 12:00 AM`);
    }
    window.setInterval(this.intervalo, 1000);
  },
  // watch: {
  //   REMAINING_SECONDS() {
  //     const element = document.querySelector(".cloack__seconds");
  //     element.classList.add("animation2");
  //   },
  //   REMAINING_SECONDS2() {
  //     const element = document.querySelector(".cloack__seconds");

  //     if (
  //       element.classList.contains("animation") &&
  //       element.classList.contains("animation2")
  //     ) {
  //       element.classList.remove("animation");
  //       element.classList.remove("animation2");
  //     }
  //     element.classList.add("animation");
  //   },
  //   REMAINING_MINUTES() {
  //     const element = document.querySelector(".cloack__minutes");
  //     element.classList.add("animation2");
  //   },
  //   REMAINING_MINUTES2() {
  //     const element = document.querySelector(".cloack__minutes");
  //     if (
  //       element.classList.contains("animation") &&
  //       element.classList.contains("animation2")
  //     ) {
  //       element.classList.remove("animation");
  //       element.classList.remove("animation2");
  //     }
  //     element.classList.add("animation");
  //   },
  //   REMAINING_HOURS() {
  //     const element = document.querySelector(".cloack__hours");
  //     element.classList.add("animation2");
  //   },
  //   REMAINING_HOURS() {
  //     const element = document.querySelector(".cloack__hours");
  //     if (
  //       element.classList.contains("animation") &&
  //       element.classList.contains("animation2")
  //     ) {
  //       element.classList.remove("animation");
  //       element.classList.remove("animation2");
  //     }
  //     element.classList.add("animation");
  //   },
  //   REMAINING_DAYS() {
  //     const element = document.querySelector(".cloack__days");
  //     element.classList.add("animation2");
  //   },
  //   REMAINING_DAYS2() {
  //     const element = document.querySelector(".cloack__days");
  //     if (
  //       element.classList.contains("animation") &&
  //       element.classList.contains("animation2")
  //     ) {
  //       element.classList.remove("animation");
  //       element.classList.remove("animation2");
  //     }
  //     element.classList.add("animation");
  //   },
  // },
  computed: {},
  methods: {
    intervalo() {
      const elementS = document.querySelector(".cloack__seconds");
      const elementM = document.querySelector(".cloack__minutes");
      const elementH = document.querySelector(".cloack__hours");
      const elementD = document.querySelector(".cloack__days");
      const MILLISECONDS_OF_A_SECOND = 1000;
      const MILLISECONDS_OF_A_MINUTE = MILLISECONDS_OF_A_SECOND * 60;
      const MILLISECONDS_OF_A_HOUR = MILLISECONDS_OF_A_MINUTE * 60;
      const MILLISECONDS_OF_A_DAY = MILLISECONDS_OF_A_HOUR * 24;
      const NOW = new Date();
      const DURATION = this.fechaObjetivo - NOW;
      if (this.state) {
        this.REMAINING_SECONDS = Math.floor(
          (DURATION % MILLISECONDS_OF_A_MINUTE) / MILLISECONDS_OF_A_SECOND
        );
        this.state = false;
        if (this.REMAINING_SECONDS != this.REMAINING_SECONDS2) {
          elementS.classList.add("animation2");
        }
      } else {
        this.REMAINING_SECONDS2 = Math.floor(
          (DURATION % MILLISECONDS_OF_A_MINUTE) / MILLISECONDS_OF_A_SECOND
        );
        this.state = true;
        if (this.REMAINING_SECONDS != this.REMAINING_SECONDS2) {
          if (
            elementS.classList.contains("animation") &&
            elementS.classList.contains("animation2")
          ) {
            elementS.classList.remove("animation");
            elementS.classList.remove("animation2");
          }
          elementS.classList.add("animation");
        }
      }
      if (this.stateM) {
        this.REMAINING_MINUTES = Math.floor(
          (DURATION % MILLISECONDS_OF_A_HOUR) / MILLISECONDS_OF_A_MINUTE
        );
        if (this.REMAINING_MINUTES != this.REMAINING_MINUTES2) {
          elementM.classList.add("animation2");
          this.stateM = false;
        }
      } else {
        this.REMAINING_MINUTES2 = Math.floor(
          (DURATION % MILLISECONDS_OF_A_HOUR) / MILLISECONDS_OF_A_MINUTE
        );
        if (this.REMAINING_MINUTES != this.REMAINING_MINUTES2) {
          this.stateM = true;
          if (
            elementM.classList.contains("animation") &&
            elementM.classList.contains("animation2")
          ) {
            elementM.classList.remove("animation");
            elementM.classList.remove("animation2");
          }
          elementM.classList.add("animation");
        }
      }
      if (this.stateH) {
        this.REMAINING_HOURS = Math.floor(
          (DURATION % MILLISECONDS_OF_A_DAY) / MILLISECONDS_OF_A_HOUR
        );
        if (this.REMAINING_HOURS != this.REMAINING_HOURS2) {
          elementH.classList.add("animation2");
          this.stateH = false;
        }
      } else {
        this.REMAINING_HOURS2 = Math.floor(
          (DURATION % MILLISECONDS_OF_A_DAY) / MILLISECONDS_OF_A_HOUR
        );
        if (this.REMAINING_HOURS != this.REMAINING_HOURS2) {
          this.stateH = true;
          if (
            elementH.classList.contains("animation") &&
            elementH.classList.contains("animation2")
          ) {
            elementH.classList.remove("animation");
            elementH.classList.remove("animation2");
          }
          elementH.classList.add("animation");
        }
      }
      if (this.stateD) {
        this.REMAINING_DAYS = Math.floor(DURATION / MILLISECONDS_OF_A_DAY);
        if (this.REMAINING_DAYS != this.REMAINING_DAYS2) {
          this.stateD = false;
          elementD.classList.add("animation2");
        }
      } else {
        this.REMAINING_DAYS2 = Math.floor(DURATION / MILLISECONDS_OF_A_DAY);
        if (this.REMAINING_DAYS != this.REMAINING_DAYS2) {
          this.stateD = true;
          if (
            elementD.classList.contains("animation") &&
            elementD.classList.contains("animation2")
          ) {
            elementD.classList.remove("animation");
            elementD.classList.remove("animation2");
          }
          elementD.classList.add("animation");
        }
      }
    },
    flip() {},
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Red+Hat+Text:wght@700&display=swap");
html {
  font-size: 62.5%;
  font-weight: 700;
}
:root {
  --grayish-blue: hsl(237, 18%, 59%);
  --Soft-red: hsl(345, 95%, 68%);
  --White: hsl(0, 0%, 100%);
  --Dark-desaturated-blue: hsl(236, 21%, 26%);
  --Very-dark-blue: hsl(235, 16%, 14%);
  --mostly-black: hsl(234, 17%, 12%);
}
* {
  box-sizing: border-box;
  margin: 0;
  font-family: "Red Hat Text", sans-serif;
}
.titles {
  width: 20%;
  text-align: center;
  color: var(--grayish-blue);
  letter-spacing: 0.2rem;
  font-size: 0.7rem;
}
main {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: var(--mostly-black);
  background-image: url("~/assets/images/bg-stars.svg");
  background-position: 50% 0%;
  background-repeat: repeat;
  animation-duration: 60s;
  animation-name: nieve;
  animation-fill-mode: both;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  transform: translateZ(5px) scale(1);
  transform-origin: 0 50%;
}
@keyframes nieve {
  from {
  }
  to {
    background-position: 50% 520%;
  }
}
h1 {
  color: var(--White);
  margin: 0 auto;
  width: fit-content;
  margin-top: 15rem;
  margin-bottom: 8rem;
  text-align: center;
  letter-spacing: 0.3em;
  width: 85%;
  font-size: 1.7rem;
}
.cloack {
  display: flex;
  width: 92%;
  margin: 0 auto;
  margin-top: 1rem;
  justify-content: space-evenly;
  height: 7%;
}
.cloack div {
  position: relative;
  color: var(--Soft-red);
  font-size: 2.9rem;
  background-color: var(--Dark-desaturated-blue);
  border-radius: 0.3rem;
  width: 20%;
  text-align: center;
  padding: 1rem 0;
  max-width: 10rem;
  box-shadow: inset 0px 1px 10px 1px var(--Very-dark-blue),0px 10px 13px -7px #000000
}
.cloack div p {
  backface-visibility: hidden;
  height: fit-content;
  position: absolute;
  margin: auto;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
.back {
  transform: rotateX(-180deg);
}
.cloack  .animation {
  animation-duration: 0.9s;
  animation-name: giro;
  transform-style: preserve-3d;
  animation-fill-mode: forwards;
}
.cloack  .animation2 {
  animation-duration: 0.9s;
  animation-name: giro2;
  transform-style: preserve-3d;
  animation-fill-mode: forwards;
  box-shadow: inset 0px 1px 10px 1px var(--Very-dark-blue),0px -10px 13px -7px #000000;
  
}
@keyframes giro {
  from {
  }
  to {
    transform: rotateX(-180deg);
    box-shadow: inset 0px 1px 10px 1px var(--Very-dark-blue),0px -10px 13px -7px #000000;
  }
}
@keyframes giro2 {
  from {
    transform: rotateX(-180deg);
  }
  to {
    transform: rotateX(-360deg);
    box-shadow: inset 0px 1px 10px 1px var(--Very-dark-blue), 0px 10px 13px -7px #000000;
  }
}
.cloack p::after {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  content: "  ";
  display: block;
  width: 0.3rem;
  height: 0.5rem;
  background-color: var(--mostly-black);
  border-top-left-radius: 50%;
  border-bottom-left-radius: 50%;
}
.cloack p::before {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  content: "  ";
  display: block;
  width: 0.3rem;
  height: 0.5rem;
  background-color: var(--mostly-black);
  border-top-right-radius: 50%;
  border-bottom-right-radius: 50%;
}
.social-networks {
  width: 100%;
  height: 15rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url("~/assets/images/pattern-hills.svg");
  background-position: center;
  background-size: cover;
  position: absolute;
  bottom: 0;
}
.facebook{
  background-image: url('~/assets/images/icon-facebook.svg');
}
.instagram{
  background-image: url('~/assets/images/icon-instagram.svg');
}
.pinterest{
  background-image: url('~/assets/images/icon-pinterest.svg');
}
a{
  display: block;
  width: 2.5rem;
  height: 2.5rem;
  margin: 0 1.5rem;
  outline: none;
  
}
a:hover{
  filter: invert(55%) sepia(57%) saturate(2999%) hue-rotate(311deg) brightness(101%) contrast(97%)
}
a span{
  width: 100%;
  height: 100%;
  display: block;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  color: red;
  
}
@media (min-width: 768px) {
  h1 {
    font-size: 4rem;
  }
  .cloack {
    height: 9%;
    width: 55%;
  }
  .cloack div p {
    font-size: 5rem;
  }
  .cloack p {
    font-size: 1rem;
  }
}
@media (min-width: 1024px) {
    h1 {
    font-size: 3rem;
  }
  .cloack {
  height: 10%;
}
.cloack div {
  max-width: 22rem;
}
}
@media (min-width: 1440px) {
    h1 {
    font-size: 3rem;
  }
  .cloack {
  height: 13%;
  width: 50%;
}
.cloack div {
  max-width: 16rem;
  
}
.cloack div p{
  font-size: 7rem;
}
.social-networks {
  height: 19.5rem;
}
}
@media (min-width: 1800px) {
  .cloack {
  width: 36%;
}
.cloack div {
  max-width: 17rem;
}
.social-networks {
  height: 26rem;
}
}
</style>>

 
