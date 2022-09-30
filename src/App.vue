<template>
  <div class="container-md">
    <div class="row">
      <div
        class="col-md-4 col-lg-4 backgnd"
        v-bind:style="{ backgroundImage: 'url(' + bg_image + ')' }"
      >
        <div
          class="cd-back-div"
          v-bind:style="{ backgroundImage: 'url(' + cdBack + ')' }"
        >
          <input
            type="number"
            v-model="cardDetails.cvv"
            class="cvv-input"
            disabled
          />
        </div>
        <div
          class="cd-front-div px-3"
          v-bind:style="{ background: 'url(' + cdFront + ')' }"
        >
          <div class="row white-circle gap-3 px-2 pt-4 pb-2">
            <div
              class="col-5 logo"
              v-bind:style="{ backgroundImage: 'url(' + logo + ')' }"
            ></div>
          </div>
          <div class="row justify-content-center cd-number py-2">
            <input
              type="text"
              v-model="cardDetails.cardNumber"
              class="cardnumber-input"
              placeholder="0000 0000 0000 0000"
              disabled
            />
          </div>
          <div class="row justify-content-between">
            <div class="col-3">
              <input
                type="text"
                v-model="cardDetails.name"
                class="cardname-input"
                placeholder="JANE APPLESEED"
                disabled
              />
            </div>
            <div class="col-2">
              <input
                type="text"
                v-model="cardDetails.expdat"
                class="cardname-input"
                disabled
                placeholder="00/00"
              />
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-7 col-lg-7 cards">
        <div class="row card-form justify-content-end align-items-center">
          <card-vue
            @updateCard="updateCard" @confirmed="formvue=false" v-if="formvue==true"
          />
          <confirm-vue v-if="formvue==false" @continue="formvue=true"/>
        </div>
        <!--<confirm-vue />-->
      </div>
    </div>
  </div>
</template>

<script>
import { flip } from "@popperjs/core";
import cdBack from "./assets/images/bg-card-back.png";
import cdFront from "./assets/images/bg-card-front.png";
import bgDesktop from "./assets/images/bg-main-desktop.png";
import bgMobile from "./assets/images/bg-main-mobile.png";
import logo from "./assets/images/card-logo.svg";
import cardVue from "./components/card.vue";
import confirmVue from "./components/Confirm.vue";
export default {
  name: "App",
  components: {
    cardVue,
    confirmVue,
  },
  data() {
    return {
      bgDesktop: bgDesktop,
      bgMobile: bgMobile,
      bg_image: "",
      cdBack: cdBack,
      cdFront: cdFront,
      logo: logo,
      formvue:true,
      cardDetails: {
        cvv: "000",
        name: "JANE APPLESEED",
        cardNumber: "0000 0000 0000 0000",
        expdat: "00/00",
      },
      cardDetails1: {
        cvv: "sdasd",
        name: "sdasdasd",
        cardNumber: "asdasdasd",
        expdatMM: "asdasdasd",
        expdatYY: "asdasdasd",
      },
    };
  },
  methods: {
    updateImage() {
      if (window.innerWidth > 400) {
        this.bg_image = bgDesktop;
      } else {
        this.bg_image = bgMobile;
      }
    },
    updateCard(e) {
      this.cardDetails1 = e;
      console.log(e);
      this.updatecardbg();
    },
    updatecardbg(){
      this.cardDetails.name=this.cardDetails1.name
      this.cardDetails.cardNumber=this.cardDetails1.cardNumber
      this.cardDetails.expdat=this.cardDetails1.expdatMM+'/'+this.cardDetails1.expdatYY
      this.cardDetails.cvv=this.cardDetails1.cvv
    }
  },
  mounted() {
    this.updateImage();
  },
  created() {
    window.addEventListener("resize", this.updateImage);
  },
  destroyed() {
    window.removeEventListener("resize", this.updateImage);
  },

  computed() {
    
  },
};
</script>

<style scoped>
.backgnd {
  position: relative;
}
.cards {
  padding: 2rem;
  position: relative;
}
.cvv-input {
  border: none;
  opacity: 1;
  text-align: right;
  color: rgb(255, 255, 255);
  background: none;
}
.white-circle {
  height: 50%;
  width: 100%;
}
.cd-number {
  padding: 0;
  margin: 0;
}
.logo {
  background-repeat: no-repeat;
  width: 4rem;
  background-size: contain;
}
.cardnumber-input {
  width: 100%;
  color: rgb(255, 255, 255);
  background: none;
  border: none;
  font-size: large;
  letter-spacing: 3px;
  margin: 0;
  padding: 0;
}
.cardname-input {
  color: rgb(255, 255, 255);
  background: none;
  border: none;
}
.backgnd> ::placeholder{
  color: white;
}

@media only screen and (max-width: 399px) {
  .backgnd {
    height: 15rem;
  }
  .cards {
    padding: 2rem;
    margin-top: 3rem;
  }
  .cd-back-div {
    position: absolute;
    left: 20%;
    top: 2rem;
    right: 0;
    width: 78%;
    height: 68%;
    background-size: contain;
    background-repeat: no-repeat;
  }
  .cd-front-div {
    position: absolute;
    left: 4%;
    top: 8rem;
    right: 0;
    width: 78%;
    height: 68%;
    background-size: contain;
    background-repeat: no-repeat;
    border-radius: 0.5rem;
  }

  .cvv-input {
    margin-left: 65%;
    margin-top: 23.5%;
    width: 10%;
    height: 5vw;
  }
}
@media only screen and (min-width: 400px) {
  .backgnd {
    width: 30rem;
    overflow: inherit;
    height: 100vh;
  }
  .cd-back-div {
    position: absolute;
    left: 55%;
    overflow-x: visible;
    width: 25rem;
    height: 14rem;
    top: 50%;
    background-size: contain;
    background-repeat: no-repeat;
  }
  .cd-front-div {
    position: absolute;
    left: 35%;
    overflow-x: visible;
    width: 25rem;
    height: 14rem;
    top: 18%;
    background-size: contain;
    background-repeat: no-repeat;
    border-radius: 0.5rem;
  }
  .ard-form {
    height: 100%;
    width: 100%;
    margin: 0 0;
    padding: 0 0;
  }
  .container-md {
    width: 100%;
    margin: 0;
    padding: 0;
  }
  .cvv-input {
    margin-left: 65%;
    margin-top: 23.5%;
    width: 10%;
  }
  .card-form {
    height: 100%;
  }
}
</style>