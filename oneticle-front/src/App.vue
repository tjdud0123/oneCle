<template>
  <div id="app" class="m-0">
    <transition
      name="fade"
      mode="out-in"
      :duration="{ enter: 400, leave: 600 }"
    >
      <router-view
        @reCreate="reCreate"
        @emitIndex="setIndex"
        :key="componentKey"
        :initialweekIndex="weekIndex"
        :initialdayIndex="dayIndex"
      ></router-view>
    </transition>
    <div v-show="showTabBar">
      <tab-bar></tab-bar>
    </div>
  </div>
</template>

<script>
import TabBar from './components/TabBar';

import Vue from 'vue';
import Buefy from 'buefy';
Vue.use(Buefy);

export default {
  name: 'App',
  components: { TabBar },
  data() {
    return {
      showTabBar: false,
      currentRoute: this.$route.name,
      componentKey: true,
      weekIndex: -1,
      dayIndex: 0,
    };
  },
  methods: {
    setShowTab(to) {
      this.showTabBar = ['HOME', 'HISTORY', 'MY'].includes(to.name)
        ? true
        : false;
    },
    reCreate() {
      this.componentKey = !this.componentKey;
    },
    setIndex(weekIndex, dayIndex) {
      this.weekIndex = weekIndex;
      this.dayIndex = dayIndex;
    },
  },
  watch: {
    $route(to, from) {
      this.setShowTab(to);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  /* border: 1px solid black; */
  max-width: 400px;
  width: 100vw;
  height: 100vh;
}
</style>
