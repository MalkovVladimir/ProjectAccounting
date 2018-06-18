<template>
  <div id="General flex-col">
      <p>Задание</p>
      <div class="widget-placeholder flex">
        <div class="flex-col flex">
          <div class="widget">asd</div>
        </div>

        <div>
          <div class="widget">1.1</div>
          <div class="widget">1.2</div>
          <div class="widget">1.3</div>  
        </div>
      </div>
  </div>
</template>

<style>
#General {
    display: flex;
    align-items: center;
    justify-content: center;
}
.widget-placeholder {
    background-color: whitesmoke;
    align-items: center;
}
.flex {
    display: flex;
}
.widget {
    display: flex;
    width: 4em;
    height: 4em;
    background-color: white;
    border: 1px solid lightslategray;
    margin: 2em;
}
.flex-col {
    flex-direction: column;
}
</style>