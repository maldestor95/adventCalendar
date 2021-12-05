<template>
  <v-app>
    <v-icon @click="drawer=!drawer" class="menuicon">mdi-menu</v-icon>
    <v-navigation-drawer
      v-model="drawer"
      absolute
      temporary
    >
    <v-icon @click="drawer=!drawer">mdi-menu</v-icon>
      <v-list-item v-for="pic in picturesFolder" :key="pic.id"
      @click="changeCalendar(pic)">
        {{ pic.name }}
      </v-list-item>
    </v-navigation-drawer>
    <advent :imgpath="picFolder"/>
  </v-app>
</template>

<script>
import advent from './components/advent.vue';

export default {
  name: 'App',
  components: {
    advent,
  },

  data: () => ({
    drawer: false,
    picturesFolder: [],
    picFolder: '',
    //
  }),
  mounted() {
    fetch('https://maldestor95.github.io/adventpics/calendar.json')
      .then((res) => res.json())
      .then((rr) => {
        console.log(rr);
        this.picturesFolder = rr.picturesFolder;
      });
    this.picFolder = localStorage.getItem('picFolder') || '';
  },
  methods: {
    changeCalendar(picFolder) {
      this.drawer = false;
      this.picFolder = picFolder.path;
      localStorage.setItem('picFolder', this.picFolder);
    },
  },
};
</script>
<style lang="scss" scoped>
  .menuicon {
    position:absolute;
    z-index: 100;
    top: 0px;
    color: red;
  }
</style>
