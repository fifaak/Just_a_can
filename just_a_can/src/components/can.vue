<template>
    <div class="can" :style="{ transform: shakeStyle }">
      <p>coke</p>
    </div>
    <p>Window X coordinate: {{ windowX }}</p>
    <p>Window Y coordinate: {{ windowY }}</p>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
  
  const windowX = ref(0);
  const windowY = ref(0);
  
  // Shake animation variables
  const shakeStyle = ref('');
  let isShaking = false;
  
  const updateWindowPosition = () => {
    windowX.value = window.screenX !== undefined ? window.screenX : window.screenLeft;
    windowY.value = window.screenY !== undefined ? window.screenY : window.screenTop;
  
    // Update shake animation style
    if (!isShaking) {
      isShaking = true;
      const randomX = windowX.value // Adjust the range as needed
      const randomY = windowY.value // Adjust the range as needed
      setTimeout(() => {
          isShaking = false;
          shakeStyle.value = `translate(${randomX}px,${randomY}px )`;
        randomX =windowX.value;
        randomY =windowY.value;
        shakeStyle.value = '';
      }, 10);
    }
  };
  
  // Use onMounted to start the interval after the component is mounted
  onMounted(() => {
    var interval = setInterval(updateWindowPosition, 10);
  
    // Optionally, you can clear the interval when the component is unmounted
    onUnmounted(() => {
      clearInterval(interval);
    });
  });
  </script>
  
  <style scoped>
  .can {
    border-top: 5px rgb(104, 104, 104) solid;
    border-bottom: 5px rgb(46, 46, 46) solid;
    border-radius: 5px;
    box-shadow: 0px 5px 10px black;
    padding-top: 20px;
    background: rgb(131, 58, 180);
    background: linear-gradient(
      90deg,
      rgba(131, 58, 180, 1) 0%,
      rgba(253, 29, 29, 1) 0%,
      rgba(0, 0, 0, 1) 100%
    );
    width: 100px;
    height: 200px;
    text-align: center;
    transition: transform 0.1s ease-in-out;
  }
  
  .can p {
    color: white;
    font-weight: bold;
    font-size: 2rem;
  }
  
  /* Add more styles as needed */
  </style>
  