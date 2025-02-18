<script>
  const menuTop = [
    "Главная страница",
    "Карта",
    "Высокоскоростной электропоезд",
    "Финансовая модель",
    "Архив",
  ];
  let selected = $state(menuTop[0]);
  function selectItem(item) {
    selected = item;
  }
</script>

<body>
  <header class="header">
    <nav class="menu menu--top">
      <ul class="menu__list">
        <li class="menu__item">
          <a href="#" class="menu__link">Главная страница</a>
        </li>
        <li class="menu__item"><a href="#" class="menu__link">Карта</a></li>
        <li class="menu__item">
          <a href="#" class="menu__link">Высокоскоростной электропоезд</a>
        </li>
        <li class="menu__item">
          <a href="#" class="menu__link">Финансовая модель</a>
        </li>
        <li class="menu__item"><a href="#" class="menu__link">Архив</a></li>
      </ul>
    </nav>
    <div class="header__inner">
      <div class="header__white-left">
        <div class="header__burger"></div>
        <div class="header__logo"></div>
        <div class="header__title">
          Система управления проектной документацией проекта ВСМ-1
        </div>
      </div>
      <nav class="menu menu--bottom">
        <ul class="menu__list">
          <li class="menu__item"><a href="#" class="menu__link">Объекты</a></li>
          <li class="menu__item"><a href="#" class="menu__link">Регионы</a></li>
          <li class="menu__item"><a href="#" class="menu__link">Этапы</a></li>
          <li class="menu__item"><a href="#" class="menu__link">Слои</a></li>
        </ul>
      </nav>
    </div>
  </header>
  <main></main>
</body>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100..900;1,100..900&display=swap");
</style>
