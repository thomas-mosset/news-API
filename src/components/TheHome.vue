<template>
  <div class="home">
    <h2 class="title">Derniers articles</h2>
    <section class="latestNews">
      <div v-for="news in latestNews" :key="news.title" class="oneNews">
        <h2 class="oneNews__title">{{ news.title }}</h2>
        <p class="oneNews__author" v-if="news.author">Par : {{ news.author }}</p>
        <img :src="news.urlToImage" :alt="news.title" class="oneNews__img">
        <span class="oneNews__link"><a :href="`${news.url}`" target="_blank" class="oneNews__link__hrefLink">Accéder à l'article</a></span>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'Home',
  created() {
    this.getNews();
  },
  data() {
    return {
      latestNews: [],
      errorMsg: "",
    };
  },
  methods: {
    getNews() {
      axios
      .get("https://newsapi.org/v2/top-headlines?country=fr&apiKey=52e0e8543949449aace6bc85cd6ba312")
      .then((response) => {
        console.log(response.data.articles);
        this.latestNews = response.data.articles;
      })
      .catch((error) => {
        console.log(error);
        this.errorMsg = "Une erreur est survenue.";
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../assets/scss/vars.scss";

.title {
  font-family: $titleFont;
  font-weight: $bold;
  font-size: 3rem;
  margin-bottom: 4rem;
  text-align: center;
}

.latestNews {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

.oneNews {
  box-sizing: border-box;
  margin: 1rem 0.5rem 4rem;
  padding: 1rem;
  border: 1px solid $dark;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  &__author {
    font-weight: $thin;
    color: $color;
    margin: 0.5rem 0 0;
    word-break: break-all;
  }

  &__img {
    width: 100%;
    margin: 0.8rem 0;
  }

  &__link {
    background: $color;
    padding: 0.5rem;
    text-align: center;

    &__hrefLink {
      color: $main;
      text-decoration: none;
    }
    
    &__hrefLink::after {
      content: '|͟↗̱|';
      margin: 0px 3px 0px 5px;
      color: $main;
    }

  }

  &__link:hover {
    background: $dark;
  }
}

/* Small screen */
@media only screen and (max-width: 800px) {
  .oneNews {
    width: 60%;
  }
}

/* Medium screen */
@media only screen and (min-width: 801px) {
  .oneNews {
    width: 25%;
  }
}

/* Big screen */
@media only screen and (min-width: 1500px) {
  .oneNews {
    width: 20%;
  }
}
</style>
