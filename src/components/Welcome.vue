<template>
  <div id="General" class="flex-col">
      <p>Завершите проводку</p>
      <div class="widget-placeholder flex">
        <div class="flex-col flex">
          <div id="div-druggable" class="widget" draggable="true" v-show="show">{{ ChosenIncomingData }}</div>
        </div>

        <div>
          <div class="widget" v-for="pair in AccountValuePairs" :key="pair.id" @drop="OnDrag">Счет {{ pair.account }}</div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      AccountValuePairs: [{
        id: 0,
        value: 'касса',
        account: '50',
        incomingData: [ 'зарплата', 'что-то' ]
      },
      {
        id: 1,
        value: 'расчетные счета',
        account: '51',
        incomingData: [ 'зачисление', 'зачисление2' ]
      },
      {
        id: 2,
        value: 'товары',
        account: '41',
        incomingData: [ 'микросхемы', 'корпуса' ]
      }],
      show: true
    }
  },
  computed: {
    ChosenIncomingData: function () {
      return this.AccountValuePairs[Math.random(4).toFixed()].incomingData[Math.random(2).toFixed()]
    }
  },
  methods: {
    OnDrag: function (event) {
      alert('DROOOOP')
      // event.target.style.display = 'none'
    }
  }
}
</script>


<style>
#General {
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid darkslategray;
    align-self: stretch;
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
    width: 6em;
    height: 6em;
    background-color: white;
    border: 1px solid lightslategray;
    margin: 2em;
    align-items: center;
    justify-content: center;
}
.flex-col {
    flex-direction: column;
}
</style>