<template>
  <div class="container mx-auto max-w-md p-4">
    <h1>Transition to height auto with Vue.js</h1>

    <div class="mt-8">
      Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
      sed diam nonumy eirmod tempor invidunt ut labore et dolore.
    </div>
    <transition-expand>
      <div v-if="expanded">
        Magna aliquyam erat, sed diam voluptua. At vero eos et
        accusam et justo duo dolores et ea rebum. Stet clita kasd
        gubergren, no sea takimata sanctus est Lorem ipsum dolor
        sit amet. Lorem ipsum dolor sit amet, consetetur
        sadipscing elitr, sed diam nonumy eirmod tempor invidunt
        ut labore et dolore magna aliquyam erat, sed diam
        voluptua. At vero eos et accusam et justo duo dolores et
        ea rebum. Stet clita kasd gubergren, no sea takimata
        sanctus est Lorem ipsum dolor sit amet.
      </div>
    </transition-expand>
    <button
      class="bg-blue hover:bg-blue-dark text-white font-bold py-2 px-4 rounded mt-4"
      @click="expanded = !expanded"
    >
      {{ expanded ? `Shrink` : `Expand` }}
    </button>
  </div>
</template>

<script>
import TransitionExpand from './components/TransitionExpand.vue';

export default {
  name: `App`,
  components: {
    TransitionExpand,
  },
  data() {
    return {
      expanded: false,
    };
  },
};
</script>

<style>
.expand-enter-active,
.expand-leave-active {
  transition-property: opacity, height;
}

.expand-enter,
.expand-leave-to {
  opacity: 0;
}
</style>
