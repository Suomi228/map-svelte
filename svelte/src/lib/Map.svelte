<script>
  import { onMount, onDestroy } from "svelte";
  import { Map } from "maplibre-gl";
  import "maplibre-gl/dist/maplibre-gl.css";
  import lineGeoJson from "../line.json";

  let map;
  let mapContainer;
  let showImages = false;
  let showPlayer = false;

  const apiKey = import.meta.env.VITE_MAP_LIBRE_API_KEY;
  const images = [
    "/Group 232.png",
    "/Group 233.png",
    "/Group 234.png",
    "/Group 235.png",
  ];

  onMount(() => {
    map = new Map({
      container: mapContainer,
      style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
      center: [36.450429, 56.595394],
      zoom: 10.6,
      attributionControl: false,
    });

    map.on("load", () => {
      map.addSource("line-source", {
        type: "geojson",
        data: lineGeoJson,
      });

      map.addLayer({
        id: "line-layer",
        type: "line",
        source: "line-source",
        paint: {
          "line-color": "#FF5733",
          "line-width": 4,
        },
      });

      map.on("click", "line-layer", () => {
        showImages = !showImages;
      });
    });
  });

  onDestroy(() => {
    map.remove();
  });

  function openPlayer() {
    showImages = false;
    showPlayer = true;
  }

  function closePlayer() {
    showPlayer = false;
  }
</script>

<div class="map" class:hide={showPlayer}>
  <div class="map__container" bind:this={mapContainer}></div>
</div>

{#if showImages}
  <div class="gallery">
    {#each images as img}
      <div class="gallery__item" on:click={openPlayer}>
        <img src={img} alt="Train route" class="gallery__image" />
      </div>
    {/each}
  </div>
{/if}

{#if showPlayer}
  <div class="player-overlay">
    <button class="player-overlay__close-btn" on:click={closePlayer}>✖</button>
    <div class="player-overlay__container">
      <iframe
        class="player-overlay__iframe"
        src="https://www.youtube.com/embed/i88lNMnpvEk?autoplay=1&rel=0&modestbranding=1&showinfo=0"
        frameborder="0"
        allow="autoplay; encrypted-media"
        allowfullscreen
      ></iframe>
    </div>
  </div>
{/if}

<style>
  @import "../styles/map.css";
</style>
