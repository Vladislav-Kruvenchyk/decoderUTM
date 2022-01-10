<template>
  <div class="app">
    <section class="app__section">
      <textarea type="text" class="utm" ref="utm">
                https://www.citrus.ua/naushniki/naushniki-samsung-galaxy-buds-live-black-671140.html?utm_medium=cpc&utm_source=hotline&utm_campaign=%D0%9D%D0%B0%D1%83%D1%88%D0%BD%D0%B8%D0%BA%D0%B8,%20%D0%B3%D0%B0%D1%80%D0%BD%D0%B8%D1%82%D1%83%D1%80%D1%8B&utm_term=Samsung%20Galaxy%20Buds%20Live%20Black%20%28SM-R180NZKA%29&utm_content=671140
            </textarea
      >
    </section>
    <section>
      <button class="get-data" ref="get-data">Get data</button>
    </section>
    <div class="app__item">
      <div class="app__section2">
        <vAppItem v-for="item in utm" :key="item.id" :app_item="item" />
      </div>
      <div class="out" ref="out"></div>
    </div>
  </div>
</template>
<script>
import vAppItem from "./components/app-item.vue";
export default {
  name: "app",
  components: {
    vAppItem,
  },
  data: () => {
    return {
      utm: [
        {
          utm_source: "источник кампании",
          id: 1,
        },
        { name: "тип трафика", id: 2 },
        { name: "название кампании", id: 3 },
        { name: "идентификатор объявления", id: 4 },
        { name: "ключевое слово", id: 5 },
      ],
    };
  },
  mounted() {
    this.$refs["get-data"].addEventListener("click", () => {
      let searchString = "";
      let s = this.$refs["utm"].value;
      let url = new URL(s);
      // console.log(url);

      // let out = (this.$refs["out"].innerHTML += `<p>HOST:${url.host}`);

      if (url.search.indexOf("&") !== -1) {
        searchString = url.search.slice(1).split("&");
      } else {
        searchString = url.search.slice(1).split("&amp;");
      }
      let res = searchValue(searchString);
      for (let key in res) {
        this.$refs["out"].innerHTML += `<p>${decodeURI(res[key])}</p>`;
        // if (this.utm[key]) {
        //   this.$refs["out"].innerHTML += `<p>${this.utm[key]} : ${decodeURI(
        //     res[key]
        //   )}</p>`;
        // } else {
        //   this.$refs["out"].innerHTML += `<p>${key} : ${decodeURI(
        //     res[key]
        //   )}</p>`;
        // }
      }
    });
    function searchValue(s) {
      return s.reduce((accum, item) => {
        item = item.split("=");
        accum[item[0]] = item[1];
        return accum;
      }, {});
    }
  },
};
</script>

<style lang="scss">
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  height: 100vh;
  &__section {
    margin: 0 auto;
  }
  &__section2 {
    display: flex;
    flex-direction: column;
  }
  &__item {
    display: flex;
    width: 100%;
    justify-content: space-evenly;
  }
}
.out {
  display: flex;
  flex-direction: column;
}
textarea {
  min-width: 1000px;
  min-height: 500px;
}
.get-data {
  padding: 20px;
}
</style>
