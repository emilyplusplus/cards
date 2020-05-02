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
      <v-card
        class="mx-auto"
        max-width="344"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-title class="headline mb-1">K ♠</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-card>
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
        console.log('onDrag left, top', transform);
        target.style.transform = transform;
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
      
    },
  }
</script>

<style scoped>
.mx-auto {
  margin: 0;
}
</style>