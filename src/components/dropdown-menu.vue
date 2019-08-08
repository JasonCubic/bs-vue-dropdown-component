<template>
  <div ref="dropdown-menu" :class="{ show: showDropdown }" aria-labelledby="dropdownMenuButton">
    <slot></slot>
  </div>
</template>

<script>
import Popper from 'popper.js';
import _ from 'lodash';
// function handleDocumentClick(event) {
//   const watchedChildren = Array.prototype.slice.call(this.$refs['click-watcher-wrapper'].children);
//   const clickResults = watchedChildren.map(el => el.contains(event.target));
//   if (clickResults.some(result => result === true)) {
//     // console.log('click was inside');
//     this.$emit('clickinside');
//   } else {
//     // console.log('click was outside');
//     this.$emit('clickoutside');
//   }
// }

// function handleMounted() {
//   // document.addEventListener('click', this.handleDocumentClick);
//   // if (!this.relatedTarget) {
//   //   this.relatedTarget
//   // }
//   console.log('this.relatedTarget: ', this.relatedTarget);
// }

// function handleBeforeDestroy() {
//   // document.removeEventListener('click', this.handleDocumentClick);
// }

function handleWatchShow(newVal) {
  if (newVal === true && this.popperWasInitialized === false) {
    this.parentEl = this.$refs['dropdown-menu'].parentNode;
    const referenceElement = _.get(this, 'reference.$el', null);
    if (_.isElement(referenceElement)) {
      this.initPopper(referenceElement);
    } else {
      this.initPopper(this.parentEl.querySelector('[data-toggle="dropdown"]'));
    }
    return;
  }
  this.showDropdown = newVal;
}


function initPopper(referenceElement) {
  // const dropdownMenuEl = ;

  const popperConfig = this.getPopperDropdownConfig(referenceElement);

  // console.log("this.$refs['dropdown-menu']: ", this.$refs['dropdown-menu']);


  this.popperHandle = new Popper(referenceElement, this.$refs['dropdown-menu'], popperConfig);


  this.popperWasInitialized = true;
  this.showDropdown = true;
}

function hasClass(el, className) {
  if (el.classList) {
    return el.classList.contains(className);
  }
  // eslint-disable-next-line prefer-template
  return new RegExp('(^| )' + className + '( |$)', 'gi').test(el.className);
}

function getPlacement() {
  // console.log('this.parentEl: ', this.parentEl);
  const AttachmentMap = {
    top: 'top-start',
    topend: 'top-end',
    bottom: 'bottom-start',
    bottomend: 'bottom-end',
    right: 'right-start',
    // RIGHTEND: 'right-end',
    left: 'left-start',
    // LEFTEND: 'left-end',
  };
  const ClassName = {
    // DISABLED: 'disabled',
    // SHOW: 'show',
    dropup: 'dropup',
    dropright: 'dropright',
    dropleft: 'dropleft',
    menuright: 'dropdown-menu-right',
    // MENULEFT: 'dropdown-menu-left',
    // POSITION_STATIC: 'position-static',
  };
  let placement = AttachmentMap.bottom;
  if (this.hasClass(this.parentEl, ClassName.dropup)) {
    placement = AttachmentMap.top;
    if (this.hasClass(this.$refs['dropdown-menu'], ClassName.menuright)) {
      placement = AttachmentMap.topend;
    }
  } else if (this.hasClass(this.parentEl, ClassName.dropright)) {
    placement = AttachmentMap.right;
  } else if (this.hasClass(this.parentEl, ClassName.dropleft)) {
    placement = AttachmentMap.left;
  } else if (this.hasClass(this.parentEl, ClassName.menuright)) {
    placement = AttachmentMap.bottomend;
  }
  // console.log('placement: ', placement);
  return placement;
}

function transformConfigBoolean(configValue) {
  if (configValue === true) {
    return true;
  }
  if (_.toLower(configValue) === 'true') {
    return true;
  }
  if (configValue === 1) {
    return true;
  }
  if (configValue === '1') {
    return true;
  }
  return false;
}


function getPopperDropdownConfig(relatedTarget) {
  const popperConfig = {
    placement: this.getPlacement(),
    modifiers: {
      offset: { offset: _.toInteger(_.get(relatedTarget, 'dataset.offset', this.defaults.offset)) },
      flip: {
        enabled: transformConfigBoolean(_.get(relatedTarget, 'dataset.flip', this.defaults.flip)),
      },
      preventOverflow: {
        boundariesElement: _.get(relatedTarget, 'dataset.boundary', this.defaults.boundary),
      },
    },
  };
  const display = _.get(relatedTarget, 'dataset.display', this.defaults.display);
  // Disable Popper.js if we have a static display
  if (display === 'static') {
    popperConfig.modifiers.applyStyle = {
      enabled: false,
    };
  }
  return popperConfig;
}

export default {
  name: 'dropdown-menu',
  props: {
    reference: {
      type: Object,
      // default: this.$refs['dropdown-menu'].parentNode,
    },
    // popperSettings: {
    //   type: Object,
    //   default: () => ({}),
    // },
    // offset: {
    //   type: Number,
    //   default: 0,
    // },
    // flip: {
    //   type: Boolean,
    //   default: true,
    // },
    // boundary: {
    //   type: String,
    //   default: 'scrollParent',
    // },
    // // reference: {
    // //   type: String,
    // //   default: 'toggle',
    // // },
    // display: {
    //   type: String,
    //   default: 'dynamic',
    // },
    show: {
      type: Boolean,
      default: false,
    },
  },
  // mounted: handleMounted,
  // beforeDestroy: handleBeforeDestroy,
  data() {
    return {
      popperWasInitialized: false,
      showDropdown: false,
      referenceEl: null,
      popperHandle: null,
      parentEl: null,
      defaults: {
        offset: 0,
        flip: true,
        boundary: 'scrollParent',
        reference: 'toggle',
        display: 'dynamic',
      },
    };
  },
  watch: {
    show: handleWatchShow,
  },
  methods: {
    initPopper,
    getPopperDropdownConfig,
    getPlacement,
    hasClass,
    transformConfigBoolean,
  },

};
</script>
