<template>
  <div id="app">
    <router-view :key="$route.fullPath"/>
  </div>
</template>

<script>
export default {
  name: 'App',
  metaInfo() {
    return {
      // if no subcomponents specify a metaInfo.title, this title will be used
      title: 'Home',
      // all titles will be injected into this template
      titleTemplate: '%s | Manga Editor',
      htmlAttrs: {
        lang: this.currentLocale,
      },
    };
  },
  computed: {
    currentLocale() {
      return this.$i18n.locale;
    },
  },
  created() {
    this.setLocale();
  },
  methods: {
    setLocale() {
      const browserLocale = navigator.language;
      let presetLocale = '';
      if (browserLocale.startsWith('zh')) {
        presetLocale = 'zh';
      } else {
        presetLocale = 'en';
      }
      const cookieLocale = this.$cookie.get('locale') || presetLocale;
      if (cookieLocale !== this.$i18n.locale) {
        this.$i18n.locale = cookieLocale;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: 'Open Sans', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
<style src="@/assets/tailwind.css"></style>
