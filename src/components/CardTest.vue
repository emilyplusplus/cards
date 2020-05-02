<template>
  <v-container>
    <Moveable
      ref="moveable"
      class="moveable"
      v-bind="moveable"
      @drag="handleDrag"
      @resize="handleResize"
      @scale="handleScale"
      @rotate="handleRotate"
      @warp="handleWarp"
      @pinch="handlePinch"
    >
      <div class="card">
        <h1>K<i class="fas fa-heart"></i></h1>
        <div class="spacer">

        </div>
        <h1 class="bottom">K<i class="fas fa-heart"></i></h1>
      </div>
    </Moveable>
  </v-container>
</template>

<script>
  import Moveable from 'vue-moveable';

  export default {
    name: 'CardTest',
    components: {
      Moveable,
    },
    data: () => ({
      moveable: {
        draggable: true,
        throttleDrag: 0,
        resizable: false,
        throttleResize: 1,
        keepRatio: false,
        scalable: false,
        throttleScale: 0,
        rotatable: false,
        throttleRotate: 0,
        pinchable: false, // ["draggable", "resizable", "scalable", "rotatable"]
        origin: false,
      }
    }),
    methods: {
      handleDrag({ target, transform }) {
        //console.log('onDrag left, top', transform);
        target.style.transform = transform;
        window.socket.emit('card_moved', transform);
      },
      handleResize({
        target, width, height, delta,
      }) {
        console.log('onResize', width, height);
        delta[0] && (target.style.width = `${width}px`);
        delta[1] && (target.style.height = `${height}px`);
      },
      handleScale({ target, transform, scale }) {
        console.log('onScale scale', scale);
        target.style.transform = transform;
      },
      handleRotate({ target, dist, transform }) {
        console.log('onRotate', dist);
        target.style.transform = transform;
      },
      handleWarp({ target, transform }) {
        console.log('onWarp', transform);
        target.style.transform = transform;
      },
      handlePinch({ target }) {
        console.log('onPinch', target);
      },
    },
    mounted() {
      window.socket.on('card_moved', function(msg){
        //console.log(msg)
        var x = document.getElementsByClassName("moveable")[0]
        x.style.transform = msg
      });
    },
  }
</script>

<style scoped>
.mx-auto {
  margin: 0;
}

.card {
  border-radius: 5px;
  width: 200px;
  height: 300px;
  box-shadow: 0 0 8px 0 #ccc;
  overflow: hidden;
  position: relative;
}

h1 {
  position: absolute;
  left: 20px;
  top: 20px;
  margin: 0;
  font-family: 'Montserrat', Arial, Helvetica, sans-serif;
  color: rgb(180, 23, 31);
}

h1 i {
  font-size: 0.85em;
  margin-left: 5px;
}

h1.bottom {
  bottom: 20px;
  right: 20px;
  transform: rotate(180deg);
}

.card .spacer {
  position: absolute;
  top: 75px;
  left: -50px;
  height: 150px;
  width: 300px;
  background: url('https://images.unsplash.com/photo-1538113300105-e51e4560b4aa?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=center&w=300&q=60');
  background-position-y: -185px;
  transform: rotate(-5deg);
  border-top: 1px solid #666;
  border-bottom: 1px solid #666;
}
</style>