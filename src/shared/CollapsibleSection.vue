<template>
    <div>
        <div class="header">
             <!-- eslint-disable-next-line vuejs-accessibility/click-events-have-key-events -->
            <span v-if="open" @click="expandORcollapseClicked()">&#x25B2; Collapse</span>
            <!-- eslint-disable-next-line vuejs-accessibility/click-events-have-key-events -->
            <span v-if="!open" @click="expandORcollapseClicked()">&#x25BC; Expand</span>
        </div>
        <slot v-if="open">
            <div>DefaultContent</div>
        </slot>
    </div>
</template>

<script>
/* eslint linebreak-style: ["error", "windows"] */
export default {
  name: 'CollapsibleSection',
  data() {
    return { open: true };
  },
  methods: {
    expandORcollapseClicked() {
      this.open = !this.open;
    },
  },
};
</script>

<style scoped>
.header{
    background-color: #bbb;
    padding: 3px;
    cursor: pointer;
}
</style>
