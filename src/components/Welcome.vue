<template>
<div id="GeneralPlaceholder" class="flex">
  <div id="General" class="flex-col">
    <div class="header flex robotoFont">  
      <div class="flex">
        Завершите проводку:
        <br />
        {{ AccountValuePairs[ChoseAccount(0, 3, false)].value }}
      </div>
    </div>

    <div class="widget-zone flex">
      <overlay v-show="!show"></overlay>
        <div class="flex-col flex">
          <div 
          id="div-draggable" 
          class="widget robotoFont" 
          draggable="true" 
          v-show="show" 
          @dragend ="OnDragEnd"
          @drag="OnDrag">
            {{ AccountValuePairs[ChoseAccount(0, 3, false)].incomingData[0] }}
          </div>
          <div v-show="!show" class="widgetGhost"></div>
        </div>  

        <div class="widget-placeholder">
          <div 
          class="container robotoFont" 
          v-for="pair in AccountValuePairs" 
          :key="pair.id" 
          :class="{dragstyle: pair.isDrag}"
          @dragover.prevent="pair.isDrag = true" 
          @dragleave="pair.isDrag = false" 
          @drop="OnDrop($event, pair.id)">
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
        value: 'Расчеты c покупателями, заказчиками',
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
        value: 'Расчеты с разными дебиторами и кредиторами',
        account: '76',
        incomingData: [ 'Учет суммы НДС в составе затрат на ремонт автомобиля', 'корпуса' ],
        isDrag: false
      }],
      show: true,
      chosenID: -1
    }
  },
  methods: {
    ChoseAccount: function (min, max, reGenerate) {
      if (this.chosenID === -1 || reGenerate) {
        var generated = Math.floor(Math.random() * (max - min)) + min

        while (generated === this.chosenID) {
          generated = Math.floor(Math.random() * (max - min)) + min
        }

        this.chosenID = generated
      }

      return this.chosenID
    },
    OnDrag: function () {
      this.show = false
    },
    OnDragEnd: function () {
      if (this.show === false) {
        this.show = true
      }
    },
    OnDrop: function (event, id) {
      if (this.chosenID !== id) {
        alert('ошибка!')
        // event.target.classList.add('incorrect')
      } else {
        alert('правильно!')
      }

      this.chosenID = this.ChoseAccount(0, 3, true)
      this.show = true
      this.isDrag = false
      this.AccountValuePairs = [{
        id: 0,
        value: 'Расчеты с персоналом по оплате труда',
        account: '70',
        incomingData: [ 'заработная плата', 'Начислены отпускные гл. бухгалтеру' ],
        isDrag: false
      },
      {
        id: 1,
        value: 'Расчеты по соц страхованию и обеспечению',
        account: '69',
        incomingData: [ 'Cтраховые взносы работнику', 'зачисление2!!!' ],
        isDrag: false
      },
      {
        id: 2,
        value: 'Общепроизводственные затраты',
        account: '25',
        incomingData: [ 'Принятие к учету материалов', 'корпуса!!!' ],
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
    align-items: center;
    justify-content: center;
    color: rgba(0, 0, 0, 0.54);
    font-weight: 400;
    z-index: 10;
    box-shadow: 0px 2px 2px rgba(0,0,0,0.24);
    flex-direction: column;
    text-align: center;
}
.header:first-child {
    padding: 1em;
}
.widget-zone {
    align-items: center;
    position: relative;
    background: linear-gradient(#89f7fe, #66a6ff);
    align-self: stretch;
    justify-content: center;
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
    text-align: center;
}
.widgetGhost {
    display: flex;
    width: 7em;
    height: 7em;
    margin: 2em;
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
.incorrect {
  animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
}
@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }
  
  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>