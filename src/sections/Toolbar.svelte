<script>
  import InputControl from "../controls/InputControl.svelte";
  import RangeControl from "../controls/RangeControl.svelte";

  export let selectedColor
  export let basics
  export let stroke

</script>

<template>
  <aside id='toolbar'>
  
    <details open id='color-preview'>
      <summary>
        Color preview
      </summary>
      <section class='content' style={`
        background-color: ${ selectedColor ?? 'transparent' }
      `}>
        <span>{ selectedColor ?? '' }</span>
      </section>
    </details>
  
    <details open>
      <summary>
        Basic Controls
      </summary>
      <section class='content'>
        <RangeControl bind:value={basics.brightness} field={{
          name: 'Brightness',
          min: 0,
          max: 100,
          suffix: '%',
        }}/>
        <RangeControl bind:value={basics.divisions} field={{
          name: 'Divisions',
          min: 3,
          max: 216
        }}/>
        <RangeControl bind:value={basics.rings} field={{
          name: 'Rings',
          min: 1,
          max: 50
        }}/>
        <RangeControl bind:value={basics.rotation} field={{
          name: 'Rotation',
          min: 0,
          max: 360,
          suffix: 'º',
        }}/>
      </section>
    </details>
  
    <details>
      <summary>
        Stroke
      </summary>
      <section class='content'>
        <InputControl name='Stroke Color'>
          <div slot='input' id='stroke-colors'>
            <div id='black' on:click={() => stroke.color = '#000'}></div>
            <div id='grey' on:click={() => stroke.color = '#888'}></div>
            <div id='white' on:click={() => stroke.color = '#fff'}></div>
          </div>
        </InputControl>
        <RangeControl bind:value={stroke.width} field={{
          name: 'Stroke Width',
          min: 0,
          max: 15,
          suffix: 'px',
        }}/>
      </section>
    </details>
    
  </aside>
</template>

<style>
  #toolbar {
    height: 100%;
    background-color: var(--bgc-alternative);
    overflow: hidden auto;
    box-shadow: rgba(0, 0, 0, 1) -2px 0px 10px 0px;
  }

  details {
    font-size: 13px;
    overflow: hidden;
    max-height: 40px;
  }
  
  details[open] {
    max-height: 99rem;
    transition: max-height 2s ease-out;
  }

  summary {
    font-weight: 600;
    height: 40px;
    line-height: 40px;
    padding: 0px 5px;
    background-color: var(--bgc-summary);
    border-bottom: 1px solid var(--c-body);
  }

  .content {
    padding: 15px;
  }

  :global(details:not([open]) .content) {
    max-height: 0;
  }

  #color-preview summary {
    pointer-events: none;
  }

  #color-preview span {
    display: inline-block;
    height: 20px;
    line-height: 20px;
  }

  #stroke-colors {
    margin-top: 3px;
    width: 100%;
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: stretch;
  }

  #stroke-colors > * {
    flex-grow: 1;
  }

  #black {
    background-color: #000;
  }
  #grey {
    background-color: #888;
  }
  #white {
    background-color: #fff;
  }

</style>