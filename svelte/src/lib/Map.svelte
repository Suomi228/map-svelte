<script>
  import { onMount, onDestroy } from "svelte";
  import { Map } from "maplibre-gl";
  import "maplibre-gl/dist/maplibre-gl.css";
  import lineGeoJson from "../line.json";
  let map;
  let mapContainer;
  let showImages = false;
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
</script>

<div class="map">
  <a href="https://www.maptiler.com" class="map__watermark">
    <img
      src="https://api.maptiler.com/resources/logo.svg"
      alt="MapTiler logo"
    />
  </a>
  <div class="map__container" bind:this={mapContainer}></div>
</div>

{#if showImages}
  <div class="gallery">
    {#each images as img}
      <div class="gallery__item">
        <img src={img} alt="Train route" class="gallery__image" />
      </div>
    {/each}
  </div>
{/if}

<style>
  @import "../styles/map.css";
</style>
