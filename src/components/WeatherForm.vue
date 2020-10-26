<template>
    <form v-on:submit.prevent="onSubmit" class="form">
        <select v-model="location" class="form__select" name="location" id="location">
          <option v-for="city in cities" :key="city" v-bind:value="city">{{city}}</option>
        </select>
        <input class="form__button" type="submit" value="Search">
      </form>
</template>

<script>
export default {
  name: "WeatherForm",
  props: ["onLocationChange"],
  data() {
    return {
      cities: ["nice", "lyon", "paris"],
      location: "paris",
      onSubmit: () => {
        console.log("submit");
        this.onLocationChange(this.location);
      }
    };
  }
};
</script>

<style>
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
</style>


