<template>
    <div id="gesture-area">
      <img id="scale-element" src="../assets/logo.png">
    </div>
</template>

<script>
import interact,{ dragMoveListener } from 'interactjs'
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted() {

var scale = 1,
    gestureArea = document.getElementById('gesture-area'),
    scaleElement = document.getElementById('scale-element'),
    resetTimeout;

interact(gestureArea)
  .gesturable({
    onstart: function (event) {
      clearTimeout(resetTimeout);
      scaleElement.classList.remove('reset');
    },
    onmove: function (event) {
      scale = scale * (1 + event.ds);

      scaleElement.style.webkitTransform =
      scaleElement.style.transform =
        'scale(' + scale + ')';

      dragMoveListener(event);
    },
    onend: function (event) {
      resetTimeout = setTimeout(reset, 1000);
      scaleElement.classList.add('reset');
    }
  })
  .draggable({ onmove: dragMoveListener });

function reset () {
  scale = 1;
  scaleElement.style.webkitTransform =
  scaleElement.style.transform =
    'scale(1)';
}
}}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="styl">
#scale-element {
  display: block;
  max-width: 100%;
  margin: auto;
}

#scale-element.reset {
  transition: -webkit-transform 0.3s ease-in-out;
  transition: transform 0.3s ease-in-out;
}

</style>
