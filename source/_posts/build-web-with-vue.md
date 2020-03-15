---
title: 'Build Web App with Vue.js'
date: 2017-07-30 13:51:04
tags:
- 学习笔记
- tech
- JavaScript
- Vue.js
---

## 1. Installing Vue.js

3 ways to install Vue.js
- CDN(Content Delivery Network): <script src="https://unpkg.com/vue"></script>
- NPM(Node Package Manager):
	- npm install vue
	- sudo npm install --global vue-cli
- Visit nodejs.org and download an installer

Start a New Project

```shell
vue init webpack compare-vue
//webpack is the template name, and compare-vue is the project name.
```

Project Configuration
![Project Configuration](https://lh3.googleusercontent.com/mWCNpDtIKwQXIVEYdTwSEF_jnkvAgpQClm4_SX_FnmTD_Q1bq7ERYggNHLdehabW3DH_7eqb8l2dspTwSOtdwsJyBmxuHFJ7jvvUUwg0ChCZuSs33yV0ZYpEbzDK805pR3k3nCVPhhEth2QQ24PPE85FhNBWzPnouhbz_L9VesO20dfuf175OoWo2eg8eo_ZA3AHBfGh2DYiYI9S53K_0SeGMnuTpfUQvD_dXxeqyAK9lsDmKjsG7sKsvbelXUBWjwfFWtstqDt4_I3NrHhDLZIcqFrP86EDDC5SIiVeLTrJ2NIoMZQJHXAAgX6pO08-0wvAwKnNYuAAUZdrBgCFol0AvGh_rtW7JhTmGNHfoXQo1F5dAjjKqkGOj0DXTPFVnsl6Ou625knUBaUU2_WVoSCElCgwLGqi1DCO8nUJ9DCIBYmSd5T4tC_QSj8yw17SaZ04iP-d1REx3Dkvw3XtFNFQv_qrMYDLWWbhzecOWs4rnbJ4MTL6DWYOrE2jIloM37Dt-VZhxgE3AJ8EdfRBBthzWpa79B8mVrwepjPltLoTCNwYkUFVEpTTA2xP7QzHlZQSg4nz7fLFZ1vsvB_NbK0NHQGwJRAbIz8wAFBj8cbEJWSPYX_byG3oBeRwwep26MH7KzfiwC_-AuK2QLgz0i2bmUB_7On23jRBzkH9prYZZQ=w1274-h629-no)

CD into the project folder and run npm install to generate packages and jsons.

```shell
cd compare-vue
npm install
```

Run a project

```shell
npm run dev
```

## 2. Vue Components

**index.html**
Start point of the project, everything of the app will be inside the div with id "app"

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>compare-vue</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  </head>
  <body>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```

**src/main.js**
Imports and new Vue project start.
```javaScript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
})

```

**App.vue**
The entry point of the app, including html, script and style
```xml
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

```

**src/router/index.js**
Define the paths of the project.

```javaScript
import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/components/Home'
import Faq from '@/components/Faq'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'Home',
      component: Home
    },
    {
      path: '/faq',
      name: 'Faq',
      component: Faq
    },
  ]
})

```


## 3. Integrating a CSS Framework

Install bulma in the project folder (compare-vue)

```shell
npm install bulma --save

```

Then import bulma in App.vue. To support sass, we have to add 'lang="sass"' in style tag, and also delete these ";" and "{}" under style tag.

```xml
<style lang="sass">
@import '../node_modules/bulma/bulma.sass'

#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>
```

Install additional packages to fully support sass.

```shell
npm install node-sass sass-loader style-loader --save-dev
```

Create mq.sass file under src folder with the following contents.

```sass
$primary: #1EC9AC !default

// Responsiveness
// 960, 1152, and 1344 have been chosen because they are divisible by both 12 and 16
$tablet: 769px !default
// 960px container + 40px
$desktop: 1000px !default
// 1152px container + 40
$widescreen: 1192px !default
// 1344px container + 40
$fullhd: 1384px !default

=mobile
  @media screen and (max-width: $tablet - 1px)
    @content

=tablet
  @media screen and (min-width: $tablet), print
    @content

=tablet-only
  @media screen and (min-width: $tablet) and (max-width: $desktop - 1px)
    @content

=desktop
  @media screen and (min-width: $desktop)
    @content

=desktop-only
  @media screen and (min-width: $desktop) and (max-width: $widescreen - 1px)
    @content

```

Then import 'mq' in App.vue.

```xml
<style lang="sass">
@import '../node_modules/bulma/bulma.sass'
@import 'mq'

#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>

```

Import mq in Home.vue and Faq.vue as well.

```xml
<style lang="sass" scoped>
@import '../mq'
</style>
```

## 4. Vue.js Navigation

Go to [bulma-Doc-Navbar](http://bulma.io/documentation/components/navbar/) to see the nav bar template.

Include `Font Awesome` in the project index.html.

```html
...
  <head>
    <meta charset="utf-8">
    <title>compare-vue</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  </head>
...
```

Then edit App.vue template tag section as follows:

```html

<template>
  <div id="app">
    <div class="nav has-shadow">
      <div class="container">
        <div class="nav-left">
          <a class="nav-item">MyCompany</a>
        </div>

        <span class="nav-toggle">
          <span></span>
          <span></span>
          <span></span>
        </span>

        <div class="nav-right nav-menu">
          <router-link to="/" class="nav-item r-item">Home</router-link>
          <router-link to="faq" class="nav-item r-item">Features</router-link>
          <router-link to="faq" class="nav-item r-item">About</router-link>
          <router-link to="faq" class="nav-item r-item">FAQ</router-link>
          <div class="nav-item">
            <p class="control">
              <a class="button is-primary is-outlined">
                <span class="icon">
                  <i class="fa fa-download"></i>
                </span>
                <span>Join Now</span>
              </a>
            </p>
          </div>
        </div>

      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

```

Edit the App.vue style tag section as follows:

```html
<style lang="sass">
@import '../node_modules/bulma/bulma.sass'
@import 'mq'

.nav
  background-color: #383838
  a:hover
    color: gray

.nav-left a
  color: #fff
  font-weight: bold

a.r-item
  color:#C1C1C1
  padding: 0.5rem 1.75rem
  +mobile
    color: gray
    &:hover
      background-color: #F1F1F1

</style>

```

## 5. Making the Navigation Function

Add `v-on:click` attribute to nav-toggle and `v-bind` to both nav-toggle and nav-menu as follows:

```html
...
<span class="nav-toggle" v-on:click="toggleNav" v-bind:class="{ 'is-active': isActive }">
...
</span>
...
<div class="nav-right nav-menu" v-bind:class="{ 'is-active': isActive }">
...
</div>
...

```


Edit the App.vue script tag content as follows:

```html
<script>
  export default {
    name: 'app',
    data: function() {
      return {
        isActive: false
      }
    },
    methods: {
      toggleNav: function() {
        this.isActive = !this.isActive;
      }
    }
  }
</script>
```

Add sass item in App.vue style section:

```css
...
.nav-toggle span
	background-color: #F1F1F1
...
```

## 6. Footer Integration

Add footer under router-view in App.vue template

```html
...
<router-view></router-view>
<footer class="footer is-primary">
 <div class="container">
    <div class="columns">
      <div class="column">
        <p>And this right here is a spiffy footer, where you can put stuff.</p>
      </div>
      <div class="column has-text-right">
        <a class="icon" href="#"><i class="fa fa-facebook"></i></a>
        <a class="icon" href="#"><i class="fa fa-twitter"></i></a>
      </div>
    </div>
  </div>
</footer>
...
```

Add styling for footer in App.vue style content

```css
...
footer
  background-color: $primary !important
  color: #fff

  .icon
    color: #fff
    margin-left: 20px
...
```


## 7. Hero Section

Go to [bulma-Doc-Hero](http://bulma.io/documentation/components/navbar/) to see the hero template.

Edit the template tag section in Home.vue as follows:

```html
<template>
  <div class="home">
    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">{{heading}}</h1>
          <div class="is-two-thirds column is-paddingless">
            <h2 class="subtitle is-4">{{subheading}}</h2>
          </div>
          <a class="button is-large is-primary" id="learn">Learn more</a>
        </div>
      </div>
    </section>
  </div>
</template>
```

Edit the script tag section to return the heading and subheading attributes as follows:

```html
<script>
export default {
  name: 'home',
  data(){
    return {
      heading: 'Soaring to new heights',
      subheading: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    }
  }
}
</script>
```

To add the background, firstly we need to add the clouds.jpg to `src/assets` folder.

Then add the sass stylings in Home.vue style tag section as follows:
```xml
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
@import '../mq'

.hero
  background: url('../assets/clouds.jpg')
  background-size: cover

  .title
    +mobile
      font-weight: bold
    +tablet
      font-size: 2.5rem
    +desktop
      font-size: 4rem
      margin-top: 2rem

h2
  margin: 1.5rem 0 2rem 0 !important
</style>
```


Now the home page looks much better!
![Home Page](https://lh3.googleusercontent.com/HkHbkesYC2xjrcP_ZBC4x7DKQZ2vKNQmAEdyzWj_t6UwD59PqTW5RfSsW4mwoa6JfBG3zRBesb6XJ6ezVyF-SLEv87jNJc1_jZ4QvgZ5bEG5eTX1rMba0pVvydy8dafG4VzoM-pxAIpXYePzU37Y7JV47yako4sqW1hUb_n14cddcoCya-NuTpkqvNj84VU9CvZ0DloOhF68nFic9oMViPbcISruarLy4Fm3MkkZppgrzj6rPvX9wX2meY0NjCjdFC734nYshL9OGeGU4_0k00wB0xmnql0o5T2wqZAN2xpYHjc_MKcS6ccjbDJabfnpRDCDDXqvl_7tIj3COhUdd5ge5-vu_M1rOzyzg50UjPFImDMpUme8rjIhDcizIPVo310DTRpChgC91AkMBb8PpSZkjqd8jFtlDMwEehhW3t7U-Ho_400zoVTa96jERh8XYk85_wW6OJAkuCrDZ0mGMge94DHuafYZ7OkPzRTvX72BAf6GvYO9beK7e3wUX_Am8FNFBvm2YxtZ2Y7MpX-n3dPYb9orR341MNHAO43bo_ktcFX8NmcLESvwZPdqxS1_EODt-J2Fw-_2pD_kexHuogmPh9uqYZoa5JwrWtX7ENLim6nEFWrjGJmzn7NcX1huDfqcGPP-C-UOOReiodjkHaEO-VPfPmmpFEsI4WsiB61Nug=w528-h166-no)

## 8. Supporting Content

Add a new section below the "hero" section in Home.vue template tag section.

```html
<template>
...
    <section class="section">
      <div class="container">
        <div class="columns pd is-desktop">
          <div class="column is-1 has-text-centered">
            <i class="fa fa-cog is-primary"></i>
          </div>
          <div class="column is-one-third-desktop">
            <p class="title"><strong>We provide superior logistics so that your business can succeed in a crazy world.</strong></p>
          </div>
          <div class="column">
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.</p>
          </div>
        </div>
      </div>

      <div class="columns pd">
        <div class="column">
          <div class="card">
            <div class="card-content">
              <p class="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
              <p class="subtitle">- Gary Simon</p>
            </div>
          </div>
        </div>
        <div class="column">
          <div class="card">
            <div class="card-content">
              <p class="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
              <p class="subtitle">- Gary Simon</p>
            </div>
          </div>
        </div>
        <div class="column">
          <div class="card">
            <div class="card-content">
              <p class="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
              <p class="subtitle">- Gary Simon</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
```

Then add additional css styling in Home.vue style tag section.

```css
.fa-cog
  font-size: 40px

#learn
  +desktop
    margin-bottom: 2rem

.pd
  +tablet
    padding: 2em 0
```

## 9. FAQ Page

Install [axios](https://github.com/mzabriskie/axios) with the following command. (Axios is a promise based HTTP client for the browser and node.js)

```shell
npm install axios --save
```

Edit the script tag section in FAQ.vue as follows:

```javaScript
import axios from 'axios';

export default {
  name: 'faq',
  data: () => ({
    faqs: [],
    errors: []
  }),

  created() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        this.faqs = response.data.slice(0, 10);
      })
      .catch(e => {
        this.errors.push(e)
      })
  }
}

```


Then edit the template tag section in FAQ.vue as follows:

```xml
<template>
  <div class="faq">
    <div class="container">
      <section class="section">
        <h1 class="title">FAQ</h1>
        <h2 class="subtitle is-4">Lorum ipsum and all of that jazz.</h2>

        <div class="columns" v-if="faqs && faqs.length">
          <div class="column is-one-third" v-for="faq of faqs">
            <div class="card">
              <div class="card-content">
                <p class="title">{{ faq.title }}</p>
                <p class="answer">{{ faq.body }}</p>
              </div>
            </div>
          </div>
        </div>

      </section>
    </div>
  </div>
</template>
```

Now the FAQ page will be look like this.
![FAQ page](https://lh3.googleusercontent.com/tT0KMI_C2pFDShdc--lzNfBMSELx64a-SYrv2pmNYUrJ7xhffKzhPUX8KiQjnSOvxp55afV-kGRCyHCuh7rt3RLNegzIWGHxXzHC8KH23REY0qScddcHB8xUAYdkKMkxgSJsWd1E8BxGRe4rx0X8jZxP3_I2s85sVVyObNWTYB2nBBHiMujYAc2MPjch-rhwJQv4OBpaP2dI50Nd1_c_TgUs34upYnvJAtbNcsg8z4n6QLgEETT2ggX7zEPtkLdG0dllo0wiUyFOPWQ_o7glM9_47CzjJcnN6Z4ZFXh0oeQnqB7OWys6izvEcn3aFygcpnlsksXr7v7ZEMsKVwamclgRvhjR2PfB0Jz4LrOc8EEGqZXpDEHLwSTCIGqirVwHqIndvkJfQWJXH410PsRCHR96CDk-u8UT_odK3kZ_uk4wISUR9MjElucm0J6FNHQARIS-fLBoxXnlbbpnDJkVIfZf3F5GkiSp1OKNkirfOZ_KUx5Lc4OqaHZjAzO__cK-SX7IiiRd7_A4FbzymSSeA2-YcO-ZI9Mo83gKqMf-K5Pb06Eao9Q392hSEYfQdDBBAUqcuCcyeNMmoMArvdCEd98nHop8jnPjPgPv7I3zqBciaE0anVPTzNxiul9Wa4WtdlFzXhH6YjTaCDOoSprci6BlgHRDl0QOBLZoJIs1TZM6vw=w1086-h691-no)
