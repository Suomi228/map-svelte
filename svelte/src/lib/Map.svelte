<script>
  import { onMount, onDestroy } from "svelte";
  import { Map } from "maplibre-gl";
  import "maplibre-gl/dist/maplibre-gl.css";
  import lineGeoJson from "../line.json"

  let map;
  let mapContainer;

  const apiKey = import.meta.env.VITE_MAP_LIBRE_API_KEY;

  onMount(() => {

    map = new Map({
      container: mapContainer,
      style: `https://api.maptiler.com/maps/streets-v2/style.json?key=${apiKey}`,
      center: [36.450429,56.595394],
      zoom: 10.6,
      attributionControl: false
    });

    map.on('load', () => {
      map.addSource('line-source', {
        type: 'geojson',
        data: lineGeoJson,
      });

      map.addLayer({
        id: 'line-layer',
        type: 'line',
        source: 'line-source',  
        paint: {
          'line-color': '#FF5733',
          'line-width': 4,
        },
      });
    });
  });

  onDestroy(() => {
    map.remove();
  });
</script>

<div class="map-wrap">
  <a href="https://www.maptiler.com" class="watermark"
    ><img
      src="https://api.maptiler.com/resources/logo.svg"
      alt="MapTiler logo"
    /></a
  >
  <div class="map" bind:this={mapContainer}></div>
</div>

<style>
  .map-wrap {
    position: relative;
    width: 100%;
    height: calc(
      100vh - 77px
    );
  }

  .map {
    position: absolute;
    width: 100%;
    height: 100%;
  }

  .watermark {
    position: absolute;
    left: 10px;
    bottom: 10px;
    z-index: 999;
  }
</style>
