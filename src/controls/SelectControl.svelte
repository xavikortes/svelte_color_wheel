<script>
  import InputControl from './InputControl.svelte';

  export let field
  export let value
</script>

<template>
  <InputControl name={field.name}>
    <select slot='input' bind:value>
      {#each field.options as option (option)}
        <option value={option}>{option}</option>
      {/each}
    </select>
  </InputControl>
</template>

<style>
  select {
    width: 90%;
    height: 26px;
    padding: 2px 4px;
    color: var(--c-inputs);
    background-color: var(--bgc-inputs);
    border: 1px solid var(--bdc-inputs);
  }
</style>