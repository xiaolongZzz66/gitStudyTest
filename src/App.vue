<template>
    <Mapview></Mapview>
</template>
<script>
import Mapview from "./views/MapContainer"
export default ({
  name:"App",
  components: {
    Mapview
  },
  setup() {
  },
})
</script>
<style >
  #app {
    height: 100%;
    width: 100%;
    padding: 0px;
    margin: 0px;
  }
</style>
