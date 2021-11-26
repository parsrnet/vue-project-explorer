<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {};
</script>

<style>
/* Animations */
@keyframes pop-in {
  0% {
    visibility: visible;
    transform: scale(0.01);
  }

  65% {
    transform: scale(1.3);
  }

  100% {
    transform: scale(1);
  }
}
@keyframes pop-out {
  0% {
    visibility: visible;
    transform: scale(1);
  }

  60% {
    transform: scale(1.25);
  }
  70% {
    transform: scale(1.3);
  }

  99% {
    visibility: visible;
    transform: scale(0.01);
  }
  100% {
    visibility: hidden;
  }
}

img,
input[type="image"] {
  image-rendering: crisp-edges;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
