<script>
  import Map from "./lib/Map.svelte";

  const menuTop = [
    "Главная страница",
    "Карта",
    "Высокоскоростной электропоезд",
    "Финансовая модель",
    "Архив",
  ];

  let selected = menuTop[0];
  let isMenuOpen = false;

  function selectItem(item) {
    selected = item;
  }

  function setMenuState() {
    isMenuOpen = !isMenuOpen;
  }
</script>

<header class="header">
  <nav class="menu menu--top">
    <ul class="menu__list">
      {#each menuTop as item (item)}
        <li class="menu__item">
          <a
            href="#"
            class="menu__link {selected === item ? 'active' : ''}"
            on:click={() => selectItem(item)}
          >
            {item}
          </a>
        </li>
      {/each}
    </ul>
  </nav>

  <div class="header__inner">
    <div class="header__white-left">
      <div class="header__burger" on:click={setMenuState}></div>
      <div class="header__logo"></div>
      <div class="header__title">
        Система управления проектной документацией проекта ВСМ-1
      </div>
    </div>

    <nav class="menu menu--bottom {isMenuOpen ? 'menu--bottom-active' : ''}">
      <ul class="menu__list">
        <li class="menu__item"><a href="#" class="menu__link">Объекты</a></li>
        <li class="menu__item"><a href="#" class="menu__link">Регионы</a></li>
        <li class="menu__item"><a href="#" class="menu__link">Этапы</a></li>
        <li class="menu__item"><a href="#" class="menu__link">Слои</a></li>
      </ul>
    </nav>
  </div>
</header>
<main>
  <Map />
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Raleway:wght@400;700&display=swap");
</style>
