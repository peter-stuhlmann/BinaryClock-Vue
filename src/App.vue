<template>
  <main>
    <div v-if="isLoading" class="init-screen">
      <div>
        Binary Clock
        <br />
        <span> Developed by Peter R. Stuhlmann | Inspired by TU Ilmenau </span>
      </div>
    </div>
    <div v-else class="board">
      <div>
        <!-- hoursZehner -->
        <div>
          <div></div>
          <div></div>
          <div :class="{ isActive: hoursZehner === 2 }"></div>
          <div :class="{ isActive: hoursZehner === 1 }"></div>
        </div>

        <!-- hoursEiner -->
        <div>
          <div :class="{ isActive: hoursEiner === 9 || hoursEiner === 8 }"></div>
          <div
            :class="{
              isActive: hoursEiner === 7 || hoursEiner === 6 || hoursEiner === 5 || hoursEiner === 4
            }"
          ></div>
          <div
            :class="{
              isActive: hoursEiner === 7 || hoursEiner === 6 || hoursEiner === 3 || hoursEiner === 2
            }"
          ></div>
          <div
            :class="{
              isActive:
                hoursEiner === 9 ||
                hoursEiner === 7 ||
                hoursEiner === 5 ||
                hoursEiner === 3 ||
                hoursEiner === 1
            }"
          ></div>
        </div>
      </div>

      <div>
        <!-- minutesZehner -->
        <div>
          <div></div>
          <div :class="{ isActive: minutesZehner === 5 || minutesZehner === 4 }"></div>
          <div :class="{ isActive: minutesZehner === 3 || minutesZehner === 2 }"></div>
          <div
            :class="{ isActive: minutesZehner === 5 || minutesZehner === 3 || minutesZehner === 1 }"
          ></div>
        </div>

        <!-- minutesEiner -->
        <div>
          <div :class="{ isActive: minutesEiner === 9 || minutesEiner === 8 }"></div>
          <div
            :class="{
              isActive:
                minutesEiner === 7 || minutesEiner === 6 || minutesEiner === 5 || minutesEiner === 4
            }"
          ></div>
          <div
            :class="{
              isActive:
                minutesEiner === 7 || minutesEiner === 6 || minutesEiner === 3 || minutesEiner === 2
            }"
          ></div>
          <div
            :class="{
              isActive:
                minutesEiner === 9 ||
                minutesEiner === 7 ||
                minutesEiner === 5 ||
                minutesEiner === 3 ||
                minutesEiner === 1
            }"
          ></div>
        </div>
      </div>
      <div>
        <!-- secondsZehner -->
        <div>
          <div></div>
          <div :class="{ isActive: secondsZehner === 5 || secondsZehner === 4 }"></div>
          <div :class="{ isActive: secondsZehner === 3 || secondsZehner === 2 }"></div>
          <div
            :class="{ isActive: secondsZehner === 5 || secondsZehner === 3 || secondsZehner === 1 }"
          ></div>
        </div>

        <!-- secondsEiner -->
        <div>
          <div :class="{ isActive: secondsEiner === 9 || secondsEiner === 8 }"></div>
          <div
            :class="{
              isActive:
                secondsEiner === 7 || secondsEiner === 6 || secondsEiner === 5 || secondsEiner === 4
            }"
          ></div>
          <div
            :class="{
              isActive:
                secondsEiner === 7 || secondsEiner === 6 || secondsEiner === 3 || secondsEiner === 2
            }"
          ></div>
          <div
            :class="{
              isActive:
                secondsEiner === 9 ||
                secondsEiner === 7 ||
                secondsEiner === 5 ||
                secondsEiner === 3 ||
                secondsEiner === 1
            }"
          ></div>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';

const currentTime = ref(new Date());
const isLoading = ref(true);

const hoursEiner = computed(() => currentTime.value.getHours() % 10);
const hoursZehner = computed(() => Math.floor(currentTime.value.getHours() / 10));
const minutesEiner = computed(() => currentTime.value.getMinutes() % 10);
const minutesZehner = computed(() => Math.floor(currentTime.value.getMinutes() / 10));
const secondsEiner = computed(() => currentTime.value.getSeconds() % 10);
const secondsZehner = computed(() => Math.floor(currentTime.value.getSeconds() / 10));

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false;
  }, 3000);

  setInterval(() => {
    currentTime.value = new Date();
  }, 1000);
});
</script>

<style scoped>
.init-screen {
  width: 100%;
  height: calc(100vh + 10px);
  display: flex;
  justify-content: center;
  align-items: center;

  & > div {
    text-align: center;
    color: #fff;
    font-size: 36px;
    opacity: 0;
    animation:
      fadeIn 0.5s ease-in-out 0.5s forwards,
      fadeOut 0.5s ease-in-out 2.5s forwards;

    & > span {
      font-size: 16px;
    }
  }
}

.board {
  height: calc(100vh + 10px);
  background: red;
  display: flex;
  opacity: 0;
  animation: fadeIn 1.5s ease-in-out forwards;
  position: absolute;
  top: -5px;
  right: -5px;
  bottom: -5px;
  left: -5px;

  & > div {
    display: flex;
    flex-flow: column wrap;
    flex: 0 0 calc(100% / 3);

    & > div {
      display: flex;
      flex-direction: column;
      height: calc(100vh + 10px);

      & > div {
        background-color: #212121;
        border: 5px solid #000;
        box-sizing: border-box;
        flex: 0 0 25%;

        &.isActive {
          background-color: #fff;
        }
      }
    }
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
