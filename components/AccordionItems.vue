<template>
  <div class="accordion__item" :class="{ active: open }">
    <button class="accordion__header" v-on:click="toggleAccordion">
      <strong>{{ header }}</strong
      ><font-awesome-icon :icon="['fas', 'angle-down']" />
    </button>
    <div
      ref="accordionBodyRef"
      :style="[open ? { 'max-height': `${height}px` } : { 'max-height': '0' }]"
      class="accordion__body"
    >
      <div class="accordion__content" v-html="body"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AccordionItems',
  data() {
    return {
      open: false,
      height: 0,
      resizeId: 0,
    }
  },
  props: {
    id: {
      type: Number,
      required: true,
    },
    header: {
      type: String,
      required: true,
    },
    body: {
      type: String,
      required: true,
    },
  },
  methods: {
    toggleAccordion() {
      // To Change open-Variable from false to true and contrariwise
      this.open = !this.open

      // To Dynamically Copy The Height it needs into the Element
      this.height = this.$refs.accordionBodyRef.scrollHeight
      this.$emit('clicked', { el: this.$el, open: this.open })
    },
    // To Dynamically Change The Height When Resizing
    onWindowResize() {
      clearTimeout(this.resizeId)
      this.resizeId = setTimeout(this.doneResizing, 500)
    },
    doneResizing() {
      console.log('Resize Event Listener Is Called 😍')
      this.height = this.$refs.accordionBodyRef.scrollHeight
    },
  },
  mounted() {
    window.addEventListener('resize', this.onWindowResize)
  },
  destroyed() {
    window.removeEventListener('resize', this.onWindowResize)
  },
}
</script>

<style lang="scss" scoped>
.accordion__header {
  display: flex;
  justify-content: space-between;
  padding: 1rem 1rem;
  width: 100%;
  background: #007bff;
  transition: 0.5s ease all;
  border: none;
  outline: none;
  border-bottom: 1px solid #54a0ff;
  box-shadow: 0px 0px 8px 2px rgba(0, 0, 0, 0.1);
  color: #f3f3f3;
  cursor: pointer;
}

.accordion__header svg {
  transition: all 0.5s ease-in-out;
}

.accordion__header {
  .active & {
    background-color: #0069d9;
  }
}

.accordion__header:hover {
  background-color: #0069d9;
  transition: 0.5s ease all;
}

.accordion__header {
  .active & svg {
    transform: rotate(180deg);
    transition: all 0.5s ease-in-out;
  }
}

.accordion__body {
  background-color: #f3f3f3;
  max-height: 0;
  overflow: hidden;
  transition: all 0.5s ease-in-out;
}

.accordion__content {
  padding: 1rem 2.5rem 1rem 2.5rem;
  ::v-deep {
    p {
      margin: 0;
    }
  }
}
</style>
