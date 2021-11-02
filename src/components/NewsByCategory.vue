<template>
  <div>
    <h1 class="title">{{ categoryName.translation }}</h1>
    <section class="latestBusinessNews">
      <div v-for="news in filteredNews" :key="news.title" class="oneNews">
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
    name: 'NewsByCategory',
    created() {
        this.getNewsFilteredByCategory();
        document.title = this.categoryName;
    },
    data() {
        return {
            categoryName: this.$route.params.slug,
            filteredNews: [],
            errorMsg: "",
            categoriesNameTranslations: [
                {
                    id: "business",
                    translation : "Business"
                },
                {
                    id: "entertainment",
                    translation : "Divertissement"
                },
                {
                    id: "health",
                    translation : "Santé"
                },
                {
                    id: "science",
                    translation : "Science"
                },
                {
                    id: "sports",
                    translation : "Sports"
                },
                {
                    id: "technology",
                    translation : "Technologie"
                },
            ]
        }
    },
    methods: {
        getNewsFilteredByCategory() {
            axios
            .get(`https://newsapi.org/v2/top-headlines?country=fr&category=${this.categoryName}&apiKey=52e0e8543949449aace6bc85cd6ba312`)
            .then((response) => {
                console.log(response.data.articles);
                this.filteredNews = response.data.articles;
            })
            .catch((error) => {
                console.log(error);
                this.errorMsg = "Une erreur est survenue.";
            });
        },
    },
    computed: {
        categoryName() {
            return this.categoriesNameTranslations.find(
                (categoryNameTranslation) => categoryNameTranslation.id === this.categoryName
            );
        },
    },
};
</script>

<style scoped lang="scss">
@import "../assets/scss/vars.scss";
.title {
  font-family: $titleFont;
  font-weight: $bold;
  font-size: 3rem;
  margin-bottom: 4rem;
  text-align: center;
}

.latestBusinessNews {
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

    &__hrefLink::after {
      content: '|͟↗̱|';
      margin: 0px 3px 0px 5px;
      color: $main;
    }

    &__hrefLink {
        color: $main;
        text-decoration: none;
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