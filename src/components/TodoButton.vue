<script setup>

</script>

<template>
        <button >
            <slot>Create</slot>
            <!-- The text between the slot tags is a default value, to be used if none is provided when the component is used -->
        </button>
</template>

<style lang="scss" scoped>
button {
    padding: 8px 16px;
    border: none;
  }
</style>