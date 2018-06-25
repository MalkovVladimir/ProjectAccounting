<template>
<div id="GeneralPlaceholder" class="flex">
  <div id="General" class="flex-col" :ref="chosenPair = AccountValuePairs[ChosenIncomingData(0, 3)]">
    <div class="header flex robotoFont">  
      <p>
        Завершите проводку:
        <br />
        поступление в {{ chosenPair.value }}
      </p>
    </div>

    <div class="widget-zone flex">
      <overlay v-show="!show"></overlay>
        <div class="flex-col flex">
          <div 
          id="div-draggable" 
          class="widget robotoFont" 
          draggable="true" 
          @drag="OnDrag"
          @dragend="OnDragEnd">
            <div v-show="show" class="flex">
              {{ chosenPair.incomingData[ChosenIncomingData(0, 2)] }}
            </div>
          </div>
        </div>  

        <div class="widget-placeholder">
          <div 
          class="container robotoFont" 
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
    OnDragEnd: function () {
      if (this.show === false) {
        this.show = true
      }
    },
    OnDrop: function () {
      alert(this.chosenPair.incomingData[0] + ' ' + this.chosenPair.incomingData[0])
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
    margin: 1em;
}
#div-draggable{
    cursor: move;
    /*border: 2px solid rgba(0,0,0,.2);*/
    border: 2px solid white;
}
#GeneralPlaceholder {
    padding-top: 3em;
    padding-bottom: 3em;
    align-items: center;
    justify-content: center;
}
#General {
    display: flex;
    align-items: center;
    justify-content: center;
    align-self: stretch;
    width: initial;
    background-color: rgba(250, 250, 250, 1);
    box-shadow: 0px 2px 2px rgba(0,0,0,0.24), 0px 0px 2px rgba(0,0,0,0.12);
}
.header {
    background-color: white;
    align-self: stretch;
    color: rgba(0, 0, 0, 0.54);
    font-weight: 400;
    z-index: 10;
    box-shadow: 0px 2px 0px 0px rgba(0,0,0,0.24);
}
.widget-zone {
    align-items: center;
    position: relative;
    background: linear-gradient(#89f7fe, #66a6ff);
}
.widget-placeholder {
    z-index: 200;
    position: relative;
}
.flex {
    display: flex;
}
.widget {
    display: flex;
    width: 7em;
    height: 7em;
    margin: 2em;
    align-items: center;
    justify-content: center;
    color: rgba(0, 0, 0, 0.87);
    border: 1px solid rgba(0, 0, 0, .03);
    box-shadow: 0px 2px 2px rgba(0,0,0,0.24), 0px 0px 2px rgba(0,0,0,0.12);
    background-color: #fff;
    font-weight: 400;
}
.container {
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(0,0,0,.1);
    border: 2px dashed rgba(255, 255, 255, 0.9);
    color: rgba(255, 255, 255, 0.9);
    width: 7em;
    height: 7em;
    margin: 2em;
}
.robotoFont {
  font-family: Roboto,"Helvetica Neue",sans-serif
}
.flex-col {
    flex-direction: column;
}
.dragstyle {
    -webkit-transform: scale(1.2);
    -ms-transform: scale(1.2);
    transform: scale(1.2);
    border: 2px dashed rgba(255, 255, 255, 0.9);
}
.overlay {
    display: flex;
    position: absolute;
    width: initial; 
    height: inherit; 
    top: 0; 
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0,0,0,0.3);
    z-index: 100;
}
</style>