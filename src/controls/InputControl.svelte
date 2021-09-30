<script>
  export let name
</script>

<template>
  <article class='control'>
    <span>{name}</span>
    <slot name='input'>
      <input />
    </slot>
    <slot name='suffix'></slot>
  </article>
</template>

<style>
  .control {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    height: 65px;
    accent-color: red;
  }
</style>