<template>
  <div class="container">
    <section class="sidebar">
    <form class="form">
        <select class="form__select" name="location" id="location">
          <option value="paris">paris</option>
          <option value="nice">nice</option>
          <option value="lyon">lyon</option>
        </select>
        <input class="form__button" type="submit" value="Search">
      </form>
      <div class="widget">
        <p class="widget__temp">30<span class="widget__temp--celcius">ºC</span></p>
        <p class="widget__date">Today</p>
        <h2 class="widget__location"><i class="material-icons icon">location_on</i> <span class="sidebar__location-text">Paris</span></h2>
    </div>
    </section>
    <main class="main">
    </main>
    
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    // HelloWorld
  }
};
</script>

<style>
.container {
  box-sizing: border-box;
  overflow: auto;
  height: 100vh;
  width: 100vw;
  background-color: #1e213a;
  color: #e7e7eb;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}

.sidebar {
  grid-column-start: 1;
  grid-column-end: 5;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 0 46px;
}

.main {
  grid-column-start: 5;
  grid-column-end: -1;
  background: #100e1d;
}

.form {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  padding-top: 40px;
}

.form__button {
  height: 64px;
  width: 30%;
  font-size: 16px;
  background-color: #3c47e9;
  border: 1px solid #3c47e9;
  color: #e7e7eb;
  cursor: pointer;
}

.form__select {
  display: inline-block;
  width: 70%;
  height: 64px;
  border: 1px solid #616475;
  padding-left: 12px;
  font-size: 16px;
  background: #1e213a;
  color: #e7e7eb;
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
}

option {
  height: 64px;
  text-transform: uppercase;
}

.widget {
  grid-column-start: 1;
  grid-column-end: 5;
  display: flex;
  align-items: center;
  /* justify-content: space-around; */
  flex-direction: column;
  padding: 0 46px;
}

.widget__location {
  font-weight: 600;
  font-size: 18px;
  line-height: 21px;
  color: #88869d;
}

.widget__location-text {
  text-transform: capitalize;
}
.widget__location-text i {
  vertical-align: bottom;
}

.widget__date {
  font-weight: 500;
  font-size: 18px;
  line-height: 21px;
  color: #88869d;
}
.widget__temp {
  font-weight: 500;
  font-size: 144px;
  line-height: 169px;
}

.widget__temp--celcius {
  font-size: 80px;
  color: #88869d;
}
</style>
