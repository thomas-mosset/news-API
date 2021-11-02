<template>
  <div>
    <header>
      <h1 id="mainTitle">News api</h1>
    </header>
    <div id="nav">
      <router-link to="/">Accueil</router-link> |
      <router-link to="/category/business">Business</router-link> |
      <router-link to="/category/entertainment">Divertissement</router-link> |
      <router-link to="/category/health">Santé</router-link> |
      <router-link to="/category/science">Science</router-link> |
      <router-link to="/category/sports">Sports</router-link> |
      <router-link to="/category/technology">Technologie</router-link>
    </div>
    <router-view :key="$route.fullPath" />
    <footer>
      <p class="footer__text">By <a href="http://www.thomasmosset.fr/" target="_blank">Thomas Mosset</a></p>
    </footer>
  </div>
</template>

<style lang="scss">
@import "./assets/scss/vars.scss";

* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: $font;
  background: $main;
  color: $dark;
}

header, footer {
  background: $color;
}

footer {
  padding: 1rem 0;
}

.footer__text {
  text-align: center;
  color: $main;
}

.footer__text a {
  color: $main;
}

.footer__text a::after {
  content: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAoAAAAKCAYAAACNMs+9AAAAQElEQVR42qXKwQkAIAxDUUdxtO6/RBQkQZvSi8I/pL4BoGw/XPkh4XigPmsUgh0626AjRsgxHTkUThsG2T/sIlzdTsp52kSS1wAAAABJRU5ErkJggg==);
  margin: 0px 3px 0px 5px;
  color: $main;
}

#mainTitle {
  font-family: $titleFont;
  font-weight: $bold;
  font-size: 4.5rem;
  color: $main;
  padding: 1rem 0;
  text-align: center;
}

#nav {
  display: flex;
  justify-content: center;
  padding: 1.5rem;
  margin-bottom: 4rem;
  border-bottom: solid 3px $color;

  a {
    font-weight: bold;
    color: $dark;
    margin: 0 0.7rem;
    text-decoration: none;

    &.router-link-exact-active {
      color: $color;
    }
  }

  a:hover {
    text-decoration: underline;
  }
}
</style>
