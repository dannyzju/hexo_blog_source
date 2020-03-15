---
title: 'Build Web App with React'
date: 2017-07-31 21:24:12
tags:
- 学习笔记
- tech
- JavaScript
- React
---

## 1. Installing React

Cd into the target folder, and run the following commands

```shell
sudo npm install -g create-react-app
```

Create a new react app called compare-react

```shell
create-react-app compare-react
```

Build and launch the project

```shell
cd compare-react
npm start
```

## 2. React Components

Initially, the app structure looks like this.

![Initial React Components](https://lh3.googleusercontent.com/wCoAPYWpnClUXMZ_Krks8XM9n31EIeow-NR5Ak9JSn2h8dDKvQvDdq15hxXc9-AYnCZJ7gGv3Ypqj2x2FDyXf0zWGbLQ-clo_MDey_NkQDsWPD8wB_L1s3P2vXzV9QW1hdg0LEKHOHGI2I0GGWQ8zbJfXE96VEI8FiklqkjT7w4Fd-toqh5iIPwYdk9o3FyFUSh7N7E5Q9sR7LFgNZuYb2LQGNRs5sBqkegRDA6M2g_yV6Ldu5dqyltNcFjd31kv0jKuyOUoqbWE5SYC26iIjGiKyJDyP1SKGG1GaVd28yYv07bzTfSas7Vg1JKQLJ3Wr57v59Bo9wJp9HN7encIpkKgYavtDH4gXOIS6_3W7qQQUV3FH0CO64nI7Uk9_zgzJvNlB2y43xCLS7RvC095fiko_k50EX_0NhIN5iU4URC4ohwLJPn2VaF4sA5Y7KPVY1Bb9o2Btu30UAQoRorQLlfTVLXDnU_y8frmyciwaSCKNRQxBdwZgBDGQUeGd6PgaEt-4Blthd7NuF_oyR3cp_ZgBIwxYd0Kg-Yidl52Rq9OXOOSJE3xt7nFgUO1uJEXZxwpHVBgT4bFoLRtbAv0MUZezpf92ZtmCPPj5wPhKgPL7kNXHKmcvPiwXUNr-PrGqlZBkQa2181v2Q863quAY2qbkg8sCuKppU-Ws3QwIAN1Mg=w2036-h956-no)

To better organize the app components, create /src/components folder, and then create subfolders `Home`, `Header`, `Footer`, and `Faq` for each UI components.

**Header.js**

Same as the App.js, Header is also a stateful UI component. Create Header.js under /src/components/Header, copy and paste code from App.js, and edit it as follows:

```javaScript
import React, { Component } from 'react';

class Header extends Component {
  render() {
    return (
      <div className="App">
        MY HEADER
      </div>
    );
  }
}

export default Header;
```

**Footer.js**

Create Footer.js under /src/components/Footer, different with Header, Footer is a stateless UI component. Instead of creating a class extending Component, we need to create a const function. See the code below.

```javaScript
import React from 'react';

const Footer = () => {
  return (
    <div className = "App" >
      MY FOOTER
    </div>
  );
};

export default Footer;
```

At last, import Header and Footer in App.js like this.

```javaScript
import React, { Component } from 'react';
import Header from './component/Header/Header';
import Footer from './component/Footer/Footer';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Header />

        <Footer />
      </div>
    );
  }
}

export default App;
```

Eventually, the app structure looks like this.

![React Components](https://lh3.googleusercontent.com/eRWIVrMMJU8UtUABtAJbkQ7M6qit-Wmkk5VNEVAcwnKphNBPYKbGSAlA24XnDshYIDmvDR91rOGZ6MuAXcazFZhBagCVr3ip-aJ3OLNtKRoyzOvH2qxPWnuma3fZxBcQKRzPx_24ypk71KU8a8yOL_X7O6QEMhKVlCwoW2gX5MVAYtTYrQ8J2ImgyXFC5omNT7ZIR9F6-TIS9DHLv3PuzJnDN8qIbZGvjjuJQfmqdie0XH9unBup4EvvayBZmktAVO29HbZ0wqaGt65SPMPssy_KKArEmOm0led9hWMndrjfQ01LcEdmYYrjUm_I9N1M00kb4WCgPFSgCCuHoJwbXAQ-mTl1cdxXwEGvgOhsn60aOcQkYWRK-DVLwspuSSTJ1qgZT5JM0YeoX6J64tdSkbS_BuNTXPtJTrF4fhs_NqEiopzY1w45ZP4oktrmYyl_SLSJQgtjDmQORznm_46uvrDanmOcid799-uHbf-Rf-SceZqsfU_oHT1mMgslb5G2VIdx97SJke4CzoMTzEXKxXJ_sczXfYyDLRF0HiyT2hYvv8uXevdfuhsXr-Ehj5n_InYTpZR0H-Gp4ZO6v3bKcQsqUEVdJjhLKd9Ng1I80vSZ7J6ipF_IOHKttx5Go8uGDnVQn8yUEiEWnGJWgTuQ_sl0syiKzv4NJgIjUAH9VlZ6eA=w2204-h1246-no)

## 3. Integrating a CSS Framework

Cd project folder and install bulma

```shell
cd compare-react
npm install bulma --save
```

To add bulma to the project, we can reference [Adding a CSS Preprocessor (Sass, Less etc.)](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc)

Edit the "scripts" section in package.json as follows:

```javaScript
"scripts": {
	"build-css": "node-sass-chokidar src/ -o src/",
	"watch-css": "npm run build-css && node-sass-chokidar src/ -o src/ --watch --recursive",
	"start-js": "react-scripts start",
	"start": "npm-run-all -p watch-css start-js",
	"build": "npm run build-css && react-scripts build",
	"test": "react-scripts test --env=jsdom",
	"eject": "react-scripts eject"
}
```

Then run the following commands

```shell
npm install --save-dev npm-run-all
npm install node-sass-chokidar --save-dev
npm start
```

Check the App.css file, and you can see that the content of App.sass has been compiled to App.css, so in our code, we can just import and reference to App.css.

The app is running with very basic header and footer now!

## 4. Header & Routing

### 4.1. Header UI

Copy and edit the header code from previous vue project to Header.js as follows.

```javaScript
import React, { Component } from 'react';

class Header extends Component {
  render() {
    return (
      <div className="App">
      <div className="nav has-shadow">
        <div className="container">
          <div className="nav-left"
            <a className="nav-item">MyCompany</a>
          </div>

          <span className="nav-toggle">
            <span></span>
            <span></span>
            <span></span>
          </span>

          <div className="nav-right nav-menu">
            <div className="nav-item">
              <p className="control">
                <a className="button is-primary is-outlined">
                  <span className="icon">
                    <i className="fa fa-download"></i>
                  </span>
                  <span>Join Now</span>
                </a>
              </p>
            </div>
          </div>

        </div>
      </div>
      </div>
    );
  }
}

export default Header;
```

Copy the previous mq.sass file from vue project to /src, and create the Header.sass file under /src/components/Header with the following content.

```sass
@import '../../mq.sass'

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
```

Then import './Header.css' in Header.js

Besides, we need to change the order of "import './App.css'" in App.js as follows to avoid the styling of Header and Footer got overridden by App.css

```javaScript
import React, { Component } from 'react';
import './App.css';
import Header from './components/Header/Header';
import Footer from './components/Footer/Footer';
...
```

### 4.2. Header Routing

Install react-router-dom.

```shell
npm install react-router-dom --save
```

Import Link in Header.js, and add links under nav-menu div as follows.

```javaScript
...
import { Link } from 'react-router-dom'
...

...
<div className="nav-right nav-menu">
	<Link to="/" className="nav-item r-item">Home</Link>
	<Link to="/faq" className="nav-item r-item">Features</Link>
	<Link to="/faq" className="nav-item r-item">About</Link>
	<Link to="/faq" className="nav-item r-item">FAQ</Link>
	<div className="nav-item">
...

```

Then edit /src/index.js to add BrowserRouter as follows.

```javaScript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
, document.getElementById('root'));
registerServiceWorker();

```

Now, create /src/components/Home/Home.js and /src/components/Faq/Faq.js as placeholders for Home and Faq page for now.

```javaScript
import React, { Component } from 'react';

class Home extends Component {
  render() {
    return (
      <div>
        HOME
      </div>
    );
  }
}

export default Home;
```

```javaScript
import React, { Component } from 'react';

class Faq extends Component {
  render() {
    return (
      <div>
        Faq
      </div>
    );
  }
}

export default Faq;
```

At last, import Home and Faq into App.js, and add Rout under Header.

```javaScript
import React, { Component } from 'react';
import './App.css';
import Header from './components/Header/Header';
import Footer from './components/Footer/Footer';
import Home from './components/Home/Home';
import Faq from './components/Faq/Faq';
import { Route } from 'react-router-dom';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Header />
          <Route exact={true} path="/" component={Home} />
          <Route path="/faq" component={Faq} />
        <Footer />
      </div>
    );
  }
}

export default App;
```

Now, the header navigation should just work!

## 5. Footer & Navigation
### 5.1. Footer UI

Create /src/components/Footer/Footer.sass and copy the footer styling from previous VUE project.

```sass
@import '../../mq.sass'

footer
  background-color: $primary !important
  color: #fff

  .icon
    color: #fff
    margin-left: 20px
```

Copy and edit the footer code from previous vue project to Footer.js as follows.

```javaScript
import React from 'react';
import './Footer.css'

const Footer = () => {
  return (
    <div>
      <footer className="footer is-primary">
        <div className="container">
          <div className="columns">
            <div className="column">
              <p>And this right here is a spiffy footer, where you can put stuff.</p>
            </div>
            <div className="column has-text-right">
              <a className="icon" href="#"><i className="fa fa-facebook"></i></a>
              <a className="icon" href="#"><i className="fa fa-twitter"></i></a>
            </div>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default Footer;
```

### 5.2. Navigation

In this section, we need to make the hamburger button work for mobile web.

Firstly, add the onClick listener for "nav-toggle" span.

```html
...
<span className="nav-toggle" onClick={this.handleClick}>
	<span></span>
	<span></span>
	<span></span>
</span>
...
```

Then add constructor and handleClick methods in Header class.

```javaScript
...
  constructor(props) {
    super(props);
    this.state = {isToggleOn: false};
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }
...
```

Besides, define a menuActive attribute in render() method.

```javaScript
...
render() {
	let menuActive = this.state.isToggleOn ? 'is-active' : '';
...

```


Then modify the nav-toggle and nav-menu divs to render the menuActive attribute.

```html
...
	<span className={'nav-toggle ' + menuActive} onClick={this.handleClick}>
...
  <div className={'nav-right nav-menu ' + menuActive}>
...
```

## 6. Home Page

Create /src/assets folder, and download the clouds.jpg there.

Create Home.sass under /src/components/Home, copy and paste the styling contents from previous VUE project.

```sass
@import '../../mq.sass'

.hero
  background: url('../../assets/clouds.jpg')
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

.fa-cog
  font-size: 40px

#learn
  +desktop
    margin-bottom: 2rem

.pd
  +tablet
    padding: 2em 0
```


Also, reference the html content from previous VUE project and update the Home.js as follows.

```javaScript
import React, { Component } from 'react';
import './Home.css';

class Home extends Component {
  render() {
    let heading = 'Soaring to new heights';
    let subheading = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.';
    return (
      <div>
        <section className="hero">
          <div className="hero-body">
            <div className="container">
              <h1 className="title">{ heading }</h1>
              <div className="is-two-thirds column is-paddingless">
                <h2 className="subtitle is-4">{ subheading }</h2>
              </div>
              <a className="button is-large is-primary" id="learn">Learn more</a>
            </div>
          </div>
        </section>

        <section className="section">
          <div className="container">
            <div className="columns pd is-desktop">
              <div className="column is-1 has-text-centered">
                <i className="fa fa-cog is-primary"></i>
              </div>
              <div className="column is-one-third-desktop">
                <p className="title"><strong>We provide superior logistics so that your business can succeed in a crazy world.</strong></p>
              </div>
              <div className="column">
                <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.</p>
              </div>
            </div>
          </div>

          <div className="columns pd">
            <div className="column">
              <div className="card">
                <div className="card-content">
                  <p className="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
                  <p className="subtitle">- Gary Simon</p>
                </div>
              </div>
            </div>
            <div className="column">
              <div className="card">
                <div className="card-content">
                  <p className="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
                  <p className="subtitle">- Gary Simon</p>
                </div>
              </div>
            </div>
            <div className="column">
              <div className="card">
                <div className="card-content">
                  <p className="title">I think it's an absolutely excellent tool for our business. I can't survive without this thing.</p>
                  <p className="subtitle">- Gary Simon</p>
                </div>
              </div>
            </div>
          </div>
        </section>
      </div>
    );
  }
}

export default Home;
```

At last, delete the content in index.css to avoid the front getting affected.

Now the home page should be the same as desinged!

## 7. FAQ Page

We still need to use the same module as previous Vue project, so  firstly install it.

```shell
npm install axios --save
```


Create Faq.sass under /src/components/Faq, copy and paste the styling contents from previous VUE project.

```sass
@import '../../mq.sass'

.pd
  padding: 2.5em 0 1.5em 0

.answer
  margin-top: 10px !important
  color: gray

.columns
  flex-wrap: wrap
```

Then edit the Faq.js as follows. Data is fetched in componentDidMount() method and saved to faqs[], and then we use {this.state.faqs.map(faq => ... )} to bind data to UI.

```javaScript
import React, { Component } from 'react';
import './Faq.css';
import axios from 'axios';

class Faq extends Component {
  constructor(props) {
    super(props);
    this.state = {
      faqs: []
    };
  }

  componentDidMount() {
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then(res => {
          const faqs = res.data.slice(0, 10);
          this.setState({ faqs });
      });
  }

  render() {
    return (
      <div>
        <div className="container">
          <section className="section">
            <h1 className="title">FAQ</h1>
            <h2 className="subtitle is-4">Lorum ipsum and all of that jazz.</h2>

            <div className="columns" v-if="faqs && faqs.length">
              {this.state.faqs.map(faq =>
                <div className="column is-one-third" v-for="faq of faqs">
                  <div className="card">
                    <div className="card-content">
                      <p className="title">{ faq.title }</p>
                      <p className="answer">{ faq.body }</p>
                    </div>
                  </div>
                </div>
              )}
            </div>

          </section>
        </div>
      </div>
    );
  }
}

export default Faq;
```

Now the FAQ page is also fully implemented!
