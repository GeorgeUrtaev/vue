<template>
  <div>
    <h1>Селектор</h1>
    <select @change="$emit('translateFunc',translatedArr,selectedValue)" v-model="selectedValue">   
        <option v-for="yazik in translatedArr" :value="yazik.lang">{{yazik.lang}}</option>
    </select>
  </div>
</template>

<script>
export default {
    props:
    {
      translatedArr: Array,
    },
    data()
    {
      return {
        selectedValue: "Ру",
      }
    },
  }
</script>

<style scoped>

</style>