<!-- eslint-disable import/no-unresolved -->
<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li class="nav-item">
            <img class="logo" src="./assets/build-a-bot-logo.png" alt="build-a-bot-logo"/>
            Build-a-Bot
          </li>
        </ul>
      </nav>
    </header>
    <main>
      <RobotBuilder />
      <!-- <Search /> -->
    </main>
  </div>
</template>

<script>
// import HomePage from './home/HomePage.vue';
// import Search from './search/Search.vue';
import RobotBuilder from './build/RobotBuilder.vue';

export default {
  name: 'App',
  components: {
    // HomePage,
    RobotBuilder,
    // Search,
  },
  methods: {
    changeUserName() {
      this.user.username = 'Fred';
    },
  },
};
</script>

<style>
  body{
    background : linear-gradient(to bottom, #555, #999);
    background-attachment: fixed;
  }
</style>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

main{
  margin: 0 auto;
  padding: 30px;
  background-color: white;
  width: 1024px;
  min-height: 300px;
}

header {
  background-color: #999;
  width: 1084px;
  margin: 0 auto;
}
ul {
  padding: 3px;
  display: flex;
}
.nav-item {
  display: inline-block;
  padding: 5px 10px;
  font-size: 22px;
  border-right: 1px solid #bbb;
}
.logo {
  vertical-align: middle;
  height: 30px;
}
</style>
