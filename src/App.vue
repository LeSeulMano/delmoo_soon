<template>
  <div class="app">
    <nav>
      <header id="header">
        <nav id="header-nav" class="header-nav">
          <ul id="ul-header">
            <li>
              <a class="router-link">Accueil</a>
            </li>
            <li>
              <a class="router-link">Cours</a>
            </li>
            <li class="nav-logo" id="nav-logo">
              <a class="router-link logo-link" id="navLogo">
                <img src="./assets/Logo_DELMOO.png" alt="Logo de l'association Delmoo" id="navLogoImg">
              </a>
            </li>
            <li>
              <a class="router-link">Podcast</a>
            </li>
            <li>
              <a class="router-link " >Shop</a>
            </li>
          </ul>
          <div class="account">
            <a class="router-link"><IonIcon name="person" class="account-icon selected"></IonIcon></a>
            <IonIcon name="log-out" class="account-icon"></IonIcon>
            <IonIcon name="document" class="account-icon"></IonIcon>
          </div>
          <div class="burger-menu" id="menu-opener" @click="menuOpener">
            <div></div>
            <div></div>
            <div></div>
          </div>
        </nav>
      </header>
      <main>
        <section id="sect9" class="common_secondary_pages">
          <div class="infos">
            <h1 txt-title="Prochainement..."></h1>
            <div class="btn btn-primary btn-icon-forward" data-aos="fade-up" data-aos-delay="500" data-aos-duration="800">
              <a class="router-link">
                <div>Retour à l'accueil</div>
                <IonIcon name="chevron-forward"></IonIcon>
              </a>
            </div>
          </div>
        </section>
      </main>
    </nav>
  </div>
</template>

<script>
import anime from "animejs";
import AOS from 'aos';
import {IonIcon} from "@ionic/vue";

export default {
  name: 'App',
  components: {
    IonIcon
  },
  mounted() {
    AOS.init();
    const screenHeight = window.innerHeight;
    document.querySelector('#sect9').style.height = screenHeight + "px";
    let titleWrapper = document.querySelector('h1');
    let titleH1 = titleWrapper.getAttribute('txt-title')
    let motH1 = 0;
    titleWrapper.appendChild(document.createElement("div"))

    titleH1.split('').forEach(item => {
      if (item == ' ') {
        titleWrapper.appendChild(document.createElement("div"))
        motH1++;
      } else {
        let span = document.createElement('span')
        span.innerHTML = item
        span.classList.add('letter')
        titleWrapper.children[motH1].appendChild(span)
      }
    });
    anime({
      targets: 'h1 .letter',
      translateX: [40, 0],
      translateZ: 0,
      opacity: [0, 1],
      easing: "easeOutExpo",
      duration: 1600,
      delay: (el, i) => 500 + 30 * i
    });
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,600;0,700;0,800;1,400;1,500;1,600;1,700;1,800&display=swap');
@import 'utils/computer/variables';
@import 'utils/computer/components';


header {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
  height: 7rem;
  width: 100%;
  background-color: $terciary-white;
  transition: .3s;

  .header-nav {

    .nav-logo {
      position: relative;
      width: 10rem;
      transition: .3s;

      img {
        position: absolute;
        transition: .3s;
        top: -3.2rem;
        left: 50%;
        transform: translateX(-50%);
        width: 7rem;
        height: 7rem;
        filter: drop-shadow(0 0 0.2rem $terciary-black);
      }
    }

    ul {
      display: flex;
      align-items: center;
      padding: 0;
      margin: 0;

      li {
        list-style: none;
        margin-right: 2.5rem;
        font-weight: 600;

        a:not(.logo-link) {
          position: relative;
          display: block;
          padding: .6rem .9rem;
          z-index: 2;
          color: $primary-red;
          font-size: $p-text;

          &.onPage {
            color: $secondary-red;
          }

          &.onPage::after {
            position: absolute;
            content: '';
            height: 2px;
            width: 50%;
            top: 80%;
            left: 50%;
            transform: translateX(-50%);
            background-color: $secondary-red;
          }
        }

        a:not(.onPage, .logo-link)::after {
          position: absolute;
          content: '';
          height: 2px;
          width: 0%;
          top: 80%;
          left: 50%;
          transform: translateX(-50%);
          background-color: $primary-red;
          transition: .3s;
        }

        a:not(.onPage):hover::after {
          width: 50%;
        }

      }
    }

    .account {
      position: relative;
      left: 60rem;
      top: -2rem;
      .account-icon{
        margin-right: .5rem;
        font-size: 1rem;
        cursor: pointer;
        color: black;

        &:not(.selected){
          display: none;
        }
      }
    }

    .burger-menu {
      display: none;
    }
  }
}

@media only screen and (max-width: 1024px) {

  header {
    display: block;
    height: 4.6rem;
    width: 100%;
    background-color: $terciary-white;
    transition: .4s;

    .header-nav {
      position: relative;
      display: block;
      width: 85%;
      margin: 0 auto;
      padding: 1.8rem 0;
      height: 1px;

      .nav-logo {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        top: 5rem;
        width: 10rem;
        transition: .4s;

        img {
          position: absolute;
          transition: .4s;
          top: -3.5rem;
          left: 50%;
          transform: translateX(-50%);
          width: 5.2rem;
          height: 5.2rem;
          filter: drop-shadow(0 0 0.2rem $terciary-black);
        }
      }

      ul {
        position: absolute;
        display: flex;
        flex-direction: column;
        justify-content: center;
        left: 50%;
        transform: translate(-50%);
        top: -1rem;
        text-align: center;
        z-index: 1;
        padding: 0;
        margin: 0;
        align-items: center;
        text-align: center;

        li {
          margin-right: 0;
          transition: .3s;
          list-style: none;
          font-weight: 600;

          a:not(.logo-link) {
            position: relative;
            display: block;
            padding: .6rem .7rem;
            z-index: 2;
            color: $primary-red;
            font-size: $p-text;

            &.onPage {
              color: $secondary-red;
            }

            &.onPage::after {
              position: absolute;
              content: '';
              height: 2px;
              width: 50%;
              top: 80%;
              left: 50%;
              transform: translateX(-50%);
              background-color: $secondary-red;
            }
          }

          a:not(.onPage)::after {
            position: absolute;
            content: '';
            height: 2px;
            width: 0%;
            top: 80%;
            left: 50%;
            transform: translateX(-50%);
            transition: .3s;
          }

          a:not(.onPage):hover::after {
            width: 50%;
          }

          .onPage::after {
            position: absolute;
            content: '';
            height: 2px;
            width: 50%;
            top: 80%;
            left: 50%;
            transform: translateX(-50%);
            background-color: $secondary-red;
          }
        }

        li:not(.nav-logo) {
          visibility: hidden;
          opacity: 0;
        }
      }

      .account {
        position: relative;
        left: 23rem;
        top: 1rem;
        .account-icon{
          margin-right: .5rem;
          font-size: 1rem;
          cursor: pointer;
          color: black;

          &:not(.selected){
            display: none;
          }
        }
      }

      .burger-menu {
        position: relative;
        left: 0;
        display: flex;
        z-index: 2;
        justify-content: space-between;
        flex-direction: column;
        height: 1.3rem;
        width: 1.8rem;

        div {
          position: relative;
          width: 100%;
          height: 2px;
          background-color: $primary-red;
          transform: skewX(30deg);
          transition: .4s;
        }
      }
    }
  }

}

#app {
  font-family: "Poppins", sans-serif;
  height: 100%;
  width: 100%;
  color: $primary-black;
  font-size: $p-text;
  overflow-x: hidden;
}

.app {
  max-width: 1920px;
  height: 100%;
  margin: 0px auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  nav{
    height: auto;
  }
}

body {
  overflow-x: hidden;
  margin: 0;
  background-color: $terciary-white;
}

#sect9 {
  overflow-y: hidden;
  padding: 0;


  &:before {
    position: absolute;
    content: "";
    height: 100%;
    width: 101%;
    bottom: -0.5rem;
    background-image: url('assets/wave4.svg');
    background-repeat: no-repeat;
    background-position-y: 100%;
    left: 50%;
    transform: translateX(-50%);
  }


  .infos {
    position: absolute;
    top: 45%;
    left: 50%;
    transform: translate(-50%, -45%);
    text-align: center;
    width: 100%;

    h1 {
      position: relative;
      width: 100%;
      margin: 0;
      margin-bottom: 2rem;
      line-height: 120%;

      > div {
        display: inline-block;

        &:not(div:last-of-type) {
          margin-right: 2rem;
        }

        span {
          font-size: $h2-text;
          color: $primary-red;
          display: inline-block;
        }

      }
    }

    h2 {
      margin: 0;
      margin-bottom: 1.5rem;

      font-size: $h5-text;
      font-weight: 700;
      color: $secondary-red;
    }

    .btn {
      margin-top: .5rem;
    }
  }

}

@media only screen and (max-width: 1024px) {

  // Taille d'écriture
  $small-text: 1.25rem;
  $p-text: 1.5rem;
  $big-text: 1.2rem;
  $h6-text: 1.7rem;
  $h5-text: 2.4rem;
  $h4-text: 2.9rem;
  $h3-text: 3.8rem;
  $h2-text: 3.1rem;
  $h1-text: 6.4rem;

  #sect9 {
    overflow-y: hidden;
    padding: 0;

    .infos {
      position: absolute;
      top: 45%;
      left: 50%;
      transform: translate(-50%, -45%);
      text-align: center;
      width: 100%;

      h1 {
        position: relative;
        width: 100%;
        margin: 0;
        margin-bottom: 2rem;
        line-height: 120%;

        > div {
          display: inline-block;

          &:not(div:last-of-type) {
            margin-right: 2rem;
          }

          span {
            font-size: $h2-text;
            color: $primary-red;
            display: inline-block;
          }

        }
      }

      h2 {
        margin: 0;
        margin-bottom: 1.5rem;

        font-size: $h5-text;
        font-weight: 700;
        color: $secondary-red;
      }

      .btn {
        margin-top: .5rem;
      }
    }

  }

}


</style>
