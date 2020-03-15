---
title: 'Build Web App with Angular'
date: 2017-08-12 15:39:22
tags:
- 学习笔记
- tech
- JavaScript
- Angular
---

## 1. Installing Angular

Install Angular
```shell
npm install -g @angular/cli
ng
```

Create new Angular project
```shell
ng new compare-angular --routing --style=sass
```

Run the default project
```shell
cd compare-angular
ng serve
```

## 2. Angular Components

Generate home and faq components

```shell
ng generate component home
ng generate component home
```

Or for short:

```shell
ng g c home
ng g c home
```

Now the app components will be look like this.

![Components](https://lh3.googleusercontent.com/QZf1TU4wEeqAVNuUPhG6DNMiR3960AffF3leem5K-6z6ycRqW5d0tYY-fLEE9c_OVQPiXyPXh5CIWq4VPczFa_1lsN8j6KRTNT0PxzCqZYF0k4Aa8QDE00MFzd6sCK3giNNJ8J942aTaoazHLJfNJZNLKaCy-RcXeui8G_iKrGvvBh7hPaOnRUhqsfmAYQjEJwSm7FW_NMmg_MPMy17QG9NcI4jqRQT6YzTSsV3ttqpxXimypQKTlle8GztTbFKx3sQw3YF6WC3N281ZXM0PzS3gg7bXAQuTNml2ZP_rnqbxPpfBUzXGC9e2UEYtt1I5UVEYmGuxtKkHchB45WIJrjM0w7C6pOuOHbLqvIpqPu3yPVzj52rxOuPeorDqB2jEbLZAueeqep__Ns1yalaXvW0POQtYXf0aV6CM3bSKNmivuQsil6yOJeEgXSa1ISMXZIy9nmHXqV6aL6oyTtBkyt_fgg4hHRfoH7LMY35TnyCAi4s5C8MbKfriKmgPP0VYnePvSRd8jdThtDREhosBqVTwKxPMsyqFAJ_wdSQSX4BPq6BVmFdnWyvTYDtL82Fv-snb24Jo8hmm_vojp6fz81dEC4c5J3wFpGhQV8nfhUxsYce-76xgUiCY4Iq7j11fXM43cp2W3Z0Yu8OjSWOe8nzzBrFHhOwInYa8s3CKE-DRvw=w1448-h1552-no)

## 3. Routing & CSS Framework Integration

### 3.1. Routing

Edit the app-routing.moduels.ts to add Home and Faq components

```shell
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { FaqComponent} from './faq/faq.component';

const routes: Routes = [
  {
    path: '',
    children: HomeComponent
  },
  {
    path: 'faq',
    children: FaqComponent
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Then edit the app.component.html page as follows:

```html
HEADER

<router-outlet></router-outlet>

FOOTER
```

Now,
http://localhost:4200 -> Home page
http://localhost:4200/faq -> Faq page

### 3.2. CSS Framework Integration

Install bumla

```shell
npm install bulma --save

```

Add bulma reference in .angular.cli.json

```shell
...
      "styles": [
        "../node_modules/bulma/bulma.sass"
        "styles.sass"
      ],
...
```

Create src/mq.sass, copy and paste the same content from previous project.

Then add font-awesome to index.html file.

```html
...
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
...
```


## 4. Header & Footer Integration
### 4.1. Header

Copy the previous header html code, and replace the HEADER in `app.component.html`.

```html
<div class="nav has-shadow">
  <div class="container">
    <div class="nav-left">
      <a routerLink="/" class="nav-item">MyCompany</a>
    </div>

    <span class="nav-toggle">
        <span></span>
        <span></span>
        <span></span>
    </span>

    <div class="nav-right nav-menu">

      <a routerLink="/" class="nav-item r-item">Home</a>
      <a class="nav-item r-item">About</a>
      <a class="nav-item r-item">Features</a>
      <a routerLink="/faq" class="nav-item r-item">FAQ</a>

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

<router-outlet></router-outlet>

FOOTER
```

Then import mq.sass in app.component.sass, and copy & paste previous sass code from Vue project.

```sass
@import '../mq'

.nav
  background-color: #383838
  a:hover
    color: gray

.nav-left a
  color: #fff
  font-weight: bold

a.r-item
  color: #C1C1C1
  padding: 0.5rem 1.75rem
  +mobile
    color: gray
    &:hover
      background-color: #F1F1F1

.nav-toggle span
  background-color: #C1C1C1

footer
  background-color: $primary !important
  color: #fff

  .icon
    color: #fff
    margin-left: 20px
```

To make the menu button work, we need to make the following change in app.component.html

```html
...
    <span class="nav-toggle" (click)="toggleNav = !toggleNav;" [ngClass]="{'is-active': toggleNav }">
        <span></span>
        <span></span>
        <span></span>
    </span>

    <div class="nav-right nav-menu" [ngClass]="{'is-active' : toggleNav }">
...
```

Also add "toggleNav" attribute in app.component.ts

```javaScript
...
export class AppComponent {
  toggleNav: false;
}
...
```


### 4.2. Footer

Just copy and paste previous footer html code to app.component.html

```html
...
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
```


## 5. Home & FAQ Page
### 5.1. Home Page

Copy and paste the home html code to home.component.html.

Then copy and paste the previous sass code to home.component.sass as follows.

```sass

@import '../../mq'

.hero
  background: url('/assets/clouds.jpg')
  background-size: cover
  animation: clouds 3s forwards

  .title
    +mobile
      font-weight: bold
    +tablet
      font-size: 2.5rem
    +desktop
      font-size: 4rem

h2
  margin: 1.5rem 0 2rem 0 !important

.fa-cog
  font-size: 40px

.pd
  +tablet
    padding: 3.5em 0
  +desktop
    padding: 5em 0

```

### 5.2. Faq Page

Firstly, edit faq.component.ts as follows

```javaScript

import { Component, OnInit } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

@Component({
  selector: 'app-faq',
  templateUrl: './faq.component.html',
  styleUrls: ['./faq.component.sass']
})
export class FaqComponent implements OnInit {

  faqs: Array<any>;

  constructor(private http:Http) {

    this.http.get('https://jsonplaceholder.typicode.com/posts')
    .map(response => response.json())
    .subscribe(res => this.faqs = res);
  }

  ngOnInit() {
  }
}

```

The edit faq.component.html to use the first 10 items from faqs as follows

```html

<div class="container">
  <section class="section">
    <h1 class="title">FAQ</h1>
    <h2 class="subtitle is-4">Lorum ipsum and all of that jazz.</h2>

    <div class="columns">
      <div class="column is-one-third" *ngFor="let faq of (faqs ? faqs.slice(0, 10): [])">
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

```

Besides, we should import HttmModule in app.module.ts like this.

```javaScript

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpModule } from '@angular/http';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { FaqComponent } from './faq/faq.component';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    FaqComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Then add the following code from previous project to faq.component.sass

```css
.pd
  padding: 2.5em 0 1.5em 0

.answer
  margin-top: 10px !important
  color: gray

.columns
  flex-wrap: wrap
```

Everything is good now!
