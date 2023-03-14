import moment from 'moment';

<template>
  <div>
  <div class="countdown">
    <div class="bar"
         :style=" showCounter ? { width: `${(seconds / 30) * 100}%`} : {width: `100%`}"
    >
    </div>
  </div>

  <div v-if="showCounter" class="remaining" >
    {{ seconds >= 10 ? `00:${seconds}` : `00:0${seconds}`}}
  </div>
  </div>
</template>

<script>
export default {
  name: "Countdown",
  props: ["seconds", "showCounter"],
}
</script>

<style>
.remaining {
  position: absolute;
  top: 15px;
  left: 0;
  text-align: center;
  color: #fff;
  width: 100%;
}
.countdown {
  background-color: red;
}
</style>