<template>
  <div class="container">
    <div class="locale-changer">
      <button :class="getButtonClass('en')" @click="changeLocale('en')">
        EN
      </button>
      <button :class="getButtonClass('fr')" @click="changeLocale('fr')">
        FR
      </button>
    </div>
    <h1>{{ $t("greeting") }}</h1>
    <h3>{{ $t("subheading") }}</h3>
    <ul>
      <li v-for="(p, i) in $t('projects')" :key="i">
        {{ p.title }} -
        <a target="_blank" :href="p.link">{{ p.link }}</a>
      </li>
    </ul>
    <hr />
    <div>
      {{ $t("footer") }} -
      <a target="_blank" href="https://www.debadeepsen.com"
        >https://www.debadeepsen.com</a
      >
    </div>
  </div>
</template>

<script>
const LS_KEY = "NUXT-I18N-LOCALE";
export default {
  mounted() {
    let currentLocale = localStorage.getItem(LS_KEY);
    if (currentLocale != null) {
      this.changeLocale(currentLocale);
    }
  },

  head() {
    return {
      title: this.$t("title"),
    };
  },

  methods: {
    changeLocale(locale) {
      this.$i18n.locale = locale;
      localStorage.setItem(LS_KEY, locale);
    },

    getButtonClass(locale) {
      if (this.$i18n.locale === locale) {
        return "locale-selected";
      }
      return "locale-unselected";
    },
  },
};
</script>

