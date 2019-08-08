<template>
  <div ref="click-watcher-wrapper">
    <slot></slot>
  </div>
</template>

<script>
function handleDocumentClick(event) {
  const watchedChildren = Array.prototype.slice.call(this.$refs['click-watcher-wrapper'].children);
  const clickResults = watchedChildren.map(el => el.contains(event.target));
  if (clickResults.some(result => result === true)) {
    // console.log('click was inside');
    this.$emit('clickinside');
  } else {
    // console.log('click was outside');
    this.$emit('clickoutside');
  }
}

function handleMounted() {
  document.addEventListener('click', this.handleDocumentClick);
}

function handleBeforeDestroy() {
  document.removeEventListener('click', this.handleDocumentClick);
}


export default {
  name: 'click-outside',
  mounted: handleMounted,
  beforeDestroy: handleBeforeDestroy,
  methods: {
    handleDocumentClick,
  },
};
</script>
