<!-- Reusable Component Example -->
<template>
  <div>
    <slot name="header"></slot>
    <p>This is the default slot content.</p>
  </div>
</template>
<script lang="ts">
export default {
  name: 'ReusableComponent',
}
</script>
