<script>
export default {
  name: `TransitionExpand`,
  functional: true,
  render(createElement, context) {
    const data = {
      props: {
        name: `expand`,
      },
      on: {
        afterEnter(element) {
          // eslint-disable-next-line no-param-reassign
          element.style.height = null;
        },
        enter(element) {
          const { width } = getComputedStyle(element);

          /* eslint-disable no-param-reassign */
          // So computed values are set immediately so we can read them.
          element.style.transition = `none`;

          element.style.width = width;
          element.style.position = `absolute`;
          element.style.visibility = `hidden`;
          element.classList.remove(`expand-enter`);
          /* eslint-enable */

          const { height } = getComputedStyle(element);

          /* eslint-disable no-param-reassign */
          element.classList.add(`expand-enter`);
          element.style.width = null;
          element.style.position = null;
          element.style.visibility = null;
          /* eslint-enable */

          // Force repaint to make sure the
          // animation is triggered correctly.
          // eslint-disable-next-line no-unused-expressions
          getComputedStyle(element).height;

          // Done changing properties, turning transitions back on.
          // eslint-disable-next-line no-param-reassign
          element.style.transition = null;
          requestAnimationFrame(() => {
            // eslint-disable-next-line no-param-reassign
            element.style.height = height;
          });
        },
        leave(element) {
          const { height } = getComputedStyle(element);

          // eslint-disable-next-line no-param-reassign
          element.style.height = height;

          // Force repaint to make sure the
          // animation is triggered correctly.
          // eslint-disable-next-line no-unused-expressions
          getComputedStyle(element).height;

          requestAnimationFrame(() => {
            // eslint-disable-next-line no-param-reassign
            element.style.height = 0;
          });
        },
        afterLeave(element) {
          // eslint-disable-next-line no-param-reassign
          element.style.height = null;
        },
      },
    };

    return createElement(`transition`, data, context.children);
  },
};
</script>

<style scoped>
* {
  will-change: height, padding-top, padding-bottom, margin-top, margin-bottom;
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}
</style>

<style>
.expand-enter-active,
.expand-leave-active {
  transition:
    height 1s ease-in-out,
    margin 1s ease-in-out,
    padding 1s ease-in-out;
  overflow: hidden;
}

.expand-enter,
.expand-leave-to {
  height: 0;
  margin-top: 0 !important;
  margin-bottom: 0 !important;
  padding-top: 0 !important;
  padding-bottom: 0 !important;
}
</style>
