<script setup>
import { ref, onMounted } from 'vue'

const dimension = ref(9)
const detailed = ref(false)

const printCoordinate = (x,y) => {
  return x === y || x + y === 1 + dimension.value ? detailed.value ? `${x-1},${y-1}` : `${x}` : ''
}


</script>

<template>
  <div class="form">
    <p>enter dimensions:</p>
    <input type="number" name="rows" class="input-form" v-model="dimension">

    <div class="detail-check">
      <input type="checkbox" name="detailed" id="detailed" v-model="detailed">  
      <label for="detailed">detailed?</label>
    </div>
  </div>

  <!-- generate grid -->

  <div class="grid-container">
    <div class="rows" v-for="(y) in dimension">
      <div class="columns" v-for="(x) in dimension">
        <div class="grid">
          <div class="corner" v-if="printCoordinate(x,y) !== '' && detailed"></div>
          {{printCoordinate(x,y)}}
        </div>
      </div>
    </div>
  </div>


</template>

<style>
@import '@/assets/base.css';

.form{
  text-align: center;
}

.input-form {
  width: 80px;
}

.detail-check {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 80px;
  margin: auto;
  margin-top: 1rem;
}

.grid-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
  margin-bottom: 20px;
}

.rows {
  display: flex;
  width: fit-content;
}

.grid {
  height: 40px;
  width: 40px;
  border: 1px solid #dadada;
  border-right: none;
  border-bottom: none;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.corner {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  border-color: transparent;
  border-style: solid;
  border-width: 3px;
  border-left-color: #008001;
  border-top-color: #008001;
}


.rows:last-child {
  border-bottom: 1px solid #dadada;
}
.columns:last-child {
  border-right: 1px solid #dadada;
}

</style>
