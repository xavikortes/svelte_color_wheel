<script>
  export let selectedColor
  export let basics
  export let stroke

  let rings = []

  $: {
    rings = new Array(basics.rings).fill(null).map((_r, i) => ({
      divisions: new Array(basics.divisions).fill(null).map((_d, j) => ({
        rotation: (360 / basics.divisions) * j,
        skew: (360 / basics.divisions) + 90,
        hue: Math.round((360 / basics.divisions) * (basics.divisions - j) * 100) / 100,
        saturation: Math.round((100 / basics.rings) * (basics.rings - i) * 100) / 100,
      }))
    }))
  }
</script>

<template>
  <article>
  
    {#each rings as ring, i (i)}
      <ul class='circle-ring' style={`
        border: ${stroke.width * 1.75}px solid ${stroke.color};
        transform: rotate(${basics.rotation}deg);
        width: calc((min(100vh - 120px, 100vw - 300px) / ${basics.rings}) * (${basics.rings} - ${i}));
        padding-bottom: calc((min(100vh - 120px, 100vw - 300px) / ${basics.rings}) * (${basics.rings} - ${i}));
        height: 0;
      `}>
        {#each ring.divisions as division, j (j)}
          <li class='circle-section' style={`
            transform: rotate(${division.rotation}deg) skewY(${division.skew}deg);
            border-left: ${stroke.width}px solid ${stroke.color};
            border-bottom: ${stroke.width}px solid ${stroke.color};
            background-color: hsl(${division.hue}, ${division.saturation}%, ${basics.brightness}%);
          `} on:click={ () => selectedColor = `hsl(${division.hue}, ${division.saturation}%, ${basics.brightness}%)`}/>
        {/each}
      </ul>
    {/each}
  
  </article>
</template>

<style>
  article {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .circle-ring {
    position: absolute;
    box-sizing: content-box;
    border-radius: 100%;
    overflow: hidden;
  }

  .circle-section {
    overflow: hidden;
    position: absolute;
    top: -50%;
    right: -50%;
    width: 100%;
    height: 100%;
    transform-origin: 0% 100%;
  }
</style>