<template>
<div id="GeneralPlaceholder" class="flex">
  <div id="General" class="flex-col" :ref="chosenPair = AccountValuePairs[ChosenIncomingData(0, 3)]">
      <overlay v-show="!show"></overlay>
      Завершите проводку:
      <p>
        поступление в {{ chosenPair.value }}
      </p>
      <div class="widget-placeholder flex">
        <div class="flex-col flex">
          <div 
          id="div-draggable" 
          class="widget" 
          draggable="true" 
          @drag="OnDrag">
            <div v-show="show" class="flex">
              {{ chosenPair.incomingData[ChosenIncomingData(0, 2)] }}
            </div>
          </div>
        </div>

        <div>
          <div 
          class="widget" 
          v-for="pair in AccountValuePairs" 
          :key="pair.id" 
          :class="{dragstyle: pair.isDrag}"
          @dragover.prevent="pair.isDrag = true" 
          @dragleave="pair.isDrag = false" 
          @drop="OnDrop">
            Счет {{ pair.account }}
          </div>
        </div>
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
        incomingData: [ 'зарплата', 'что-то' ],
        isDrag: false
      },
      {
        id: 1,
        value: 'расчетные счета',
        account: '51',
        incomingData: [ 'зачисление', 'зачисление2' ],
        isDrag: false
      },
      {
        id: 2,
        value: 'товары',
        account: '41',
        incomingData: [ 'микросхемы', 'корпуса' ],
        isDrag: false
      }],
      show: true
    }
  },
  methods: {
    ChosenIncomingData: function (min, max) {
      return Math.floor(Math.random() * (max - min)) + min
    },
    OnDrag: function () {
      this.show = false
    },
    OnDrop: function () {
      this.show = true
      this.isDrag = false
      this.AccountValuePairs = [{
        id: 0,
        value: 'касса!!!',
        account: '50!!!',
        incomingData: [ 'зарплата!!!', 'что-то!!!' ],
        isDrag: false
      },
      {
        id: 1,
        value: 'расчетные счета!!!',
        account: '51!!!',
        incomingData: [ 'зачисление!!!', 'зачисление2!!!' ],
        isDrag: false
      },
      {
        id: 2,
        value: 'товары!!!',
        account: '41!!!',
        incomingData: [ 'микросхемы!!!', 'корпуса!!!' ],
        isDrag: false
      }]
    }
  },
  components: {
    overlay: {
      template: '<div class="overlay"></div>'
    }
  }
}
</script>


<style>
p {
    margin-bottom: 0px;
}
#div-draggable{
    cursor: move;
}
#GeneralPlaceholder {
    margin-top: 3em;
    align-items: center;
    justify-content: center;
}
#General {
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid darkslategray;
    align-self: stretch;
    width: initial;
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
    z-index: 200;
}
.flex-col {
    flex-direction: column;
}
.dragstyle {
    background-color: lightgoldenrodyellow;
}
.overlay {
    display: flex;
    position: absolute;
    width: 100%; 
    height: 100%; 
    top: 0; 
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0,0,0,0.3);
    z-index: 100;
}
</style>