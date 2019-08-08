<template>
  <div class="container" id="app">

      <!-- TODO: make bs-dropdown-menu it will add popper for the styles -->
      <!-- look in bs-components\src\components\bs-dropdown\bs-dropdown.tsx -->

    <!-- <div class="dropdown" :class="{ show: showMyDropdown }" is="ClickWatcher" v-on:clickoutside="showMyDropdown = false">
      <button
        class="btn btn-secondary dropdown-toggle"
        type="button"
        id="dropdownMenuButton"
        @click="showMyDropdown = !showMyDropdown"
        aria-haspopup="true"
        :aria-expanded="showMyDropdown ? 'true' : 'false'"
      >
        Dropdown button
      </button>
      <div :class="{ 'dropdown-menu': true, show: showMyDropdown }" aria-labelledby="dropdownMenuButton">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p>
    <p>&nbsp;</p> -->

    <h2>Dropdowns</h2>

    <div class="dropdown" :class="{ show: showOtherDropdown }" is="ClickWatcher" v-on:clickoutside="showOtherDropdown = false">
      <button
        class="btn btn-secondary dropdown-toggle"
        type="button"
        id="dropdownMenuButton"
        @click="showOtherDropdown = !showOtherDropdown"
        aria-haspopup="true"
        :aria-expanded="showOtherDropdown ? 'true' : 'false'"
        data-toggle="dropdown"
      >
        Dropdown button
      </button>
      <div class="dropdown-menu" is="DropdownMenu" :show="showOtherDropdown">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>

    <!-- <p>showMyDropdown: {{ showMyDropdown }}</p> -->


    <div class="dropdown" :class="{ show: s1 }" is="ClickWatcher" v-on:clickoutside="s1 = false">
      <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" @click="s1 = !s1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        Dropdown button
      </button>
      <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" is="DropdownMenu" :show="s1">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>
    <p>&nbsp;</p>

    <div class="dropdown" :class="{ show: s2 }" is="ClickWatcher" v-on:clickoutside="s2 = false">
      <a class="btn btn-secondary dropdown-toggle" @click.prevent="s2 = !s2" role="button" id="dropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        Dropdown link
      </a>
      <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" is="DropdownMenu" :show="s2">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>
    <p>&nbsp;</p>


    <div class="btn-group dropright" :class="{ show: s3 }" is="ClickWatcher" v-on:clickoutside="s3 = false">
      <button type="button" class="btn btn-info dropdown-toggle"  @click="s3 = !s3" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">dropright</button>
      <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" is="DropdownMenu" :show="s3">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>

    <div class="btn-group dropup" :class="{ show: s4 }" is="ClickWatcher" v-on:clickoutside="s4 = false">
      <button type="button" class="btn btn-secondary" ref="s4-dropup">
        Split dropup
      </button>
      <button type="button" class="btn btn-secondary dropdown-toggle dropdown-toggle-split" @click="s4 = !s4" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
        <span class="sr-only">Toggle Dropdown</span>
      </button>
      <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" is="DropdownMenu" :show="s4">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>

    <div class="btn-group dropleft" :class="{ show: s5 }" is="ClickWatcher" v-on:clickoutside="s5 = false">
      <button type="button" class="btn btn-success dropdown-toggle"  @click="s5 = !s5" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">dropleft</button>
      <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" is="DropdownMenu" :show="s5">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
      </div>
    </div>


    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import ClickWatcher from './components/click-watcher.vue';
import DropdownMenu from './components/dropdown-menu.vue';
// import HelloWorld from './components/HelloWorld.vue';

// an example:  https://github.com/mdbootstrap/Vue-Bootstrap-with-Material-Design/blob/master/src/components/Components/Dropdown.vue

export default {
  name: 'app',
  data() {
    return {
      showMyDropdown: false,
      showOtherDropdown: false,
      s1: false,
      s2: false,
      s3: false,
      s4: false,
      s5: false,
    };
  },
  components: {
    // HelloWorld,
    ClickWatcher,
    DropdownMenu,
  },
};
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
