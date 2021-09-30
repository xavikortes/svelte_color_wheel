<script lang='ts'>
  import Header from "./sections/Header.svelte";
  import Wheel from "./sections/Wheel.svelte";
  import Toolbar from "./sections/Toolbar.svelte";
  import Footer from "./sections/Footer.svelte";

  import data from './initial-data'

  let selectedColor = data.initialColor
  let basics = data.basics
  let stroke = data.stroke
</script>

<template>
  <Header />
  <main>
    <Wheel bind:selectedColor {basics} {stroke} />
    <Toolbar {selectedColor} bind:basics bind:stroke />
  </main>
  <Footer />
</template>

<style>
  :global(:root) {
    --bgc-body: #1e1e1e;
    --bgc-alternative: #252526;
    --bgc-summary: #80808024;
    --bgc-inputs: #444;

    --c-body: #e7e7e7;
    --c-inputs: #c9d1d9;

    --bdc-inputs: #30363d;
  }

  :global(body) {
    font-size: 10px;
    font-family: system-ui, Ubuntu, Droid Sans, sans-serif;
    
    color: var(--c-body);
    background-color: var(--bgc-body);

    width: 100vw;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  main {
    flex-grow: 1;
    display: grid;
    grid-template-columns: auto 300px;
    overflow: hidden auto;
  }
</style>
