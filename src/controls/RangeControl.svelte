<script>
  import InputControl from './InputControl.svelte';

  export let field
  export let value
</script>

<template>
  <InputControl name={field.name}>
    <input slot='input' type=range min={field.min} max={field.max} step={field.step ?? 1} bind:value />
    <span slot='suffix'>{ value }{ field.suffix ?? '' }</span>
  </InputControl>
</template>

<style>
  input[type='range'] {
    width: 90%;
    height: 4px;
    background-color: var(--bgc-inputs);
    border-radius: 10px;
    appearance: none;
    -webkit-appearance: none;
  }
</style>