<template>
  <div id="app">
    <ul class="fixed-top list-group m-1" style="margin-top: 100px !important; width: 170px; height: 300px;overflow: auto;">
      <li v-for="f in even(alnLst)" class="list-group-item p-1">
        {{f.alanNo}}
        {{f.left}}
        {{f.top}}
      </li>
    </ul>
    <div class="container">
      <div class="row">
        <div class="col-md-3">
          <div ref="container">
            <b-button @click="onClick">Alan Ekle {{gelen}}</b-button>
            <b-button @click="onPdf">PDF</b-button>
          </div>
        </div>
        <div class="col-md-3">
          <app-result :counter="counter"></app-result>
        </div>
        <div class="col-md-3">
          <app-second-result :counter="counter"></app-second-result>
        </div>
        <div class="col-md-3">
          <app-counter @counterEvent="counter += $event"></app-counter>
        </div>
      </div>
    </div>
    <div id="pdf" style="width: 200mm; height: 287mm; border: .1mm solid #000000;position:relative;">
      <h1 class="text-center">Test işlemi</h1>
      <div class="row" style="border: .1mm solid #000000; width: 50mm;height: 40mm;position: absolute;left: 10mm; top:30mm;"></div>
      <div class="row" style="border: .025em solid #000000; width: 50mm;height: 40mm;position: absolute;left: 70mm; top:30mm;"></div>
      <div class="row" style="border: .035em solid #000000; width: 50mm;height: 40mm;position: absolute;left: 10mm; top:80mm;"></div>
      <div class="row" style="border: .045em solid #000000; width: 50mm;height: 40mm;position: absolute;left: 70mm; top:80mm;"></div>
      <div class="row" style="border: .055em solid #000000; width: 50mm;height: 40mm;position: absolute;left: 10mm; top:130mm;"></div>
      <div class="row" style="border: .065em solid #000000; width: 50mm;height: 40mm;position: absolute;left: 70mm; top:130mm;"></div>
      <h1 class="text-center" style="top: 200mm; position: absolute;width: 100%">footer</h1>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Result from "./components/Result"
import SecondResult from "./components/SecondResult"
import Counter from "./components/Counter"
import Button from './components/Button'

import html2canvas from 'html2canvas'
import * as JsPDF from 'jspdf'

export default {
  name: 'app',
  components: {
    appResult: Result,
    appSecondResult: SecondResult,
    appCounter: Counter,
    Button
  },
  data() {
    return {
      alaNo:0,
      gelen:"",
      alnLst: []
    };
  },
  methods: {
    even: function(arr) {
      // Set slice() to avoid to generate an infinite loop!
      return arr.slice().sort(function(a, b) {
        return a.name - b.name;
      });
    },
    onPdf(){
      html2canvas(document.querySelector('#pdf'), {imageTimeout: 5000, useCORS: true}).then(canvas => {
        //document.getElementById('pdf').appendChild(canvas)
        let img = canvas.toDataURL('image/png')
        let pdf = new JsPDF('portrait', 'mm', 'a4')
        pdf.addImage(img, 'JPEG', 5, 5, 200, 287)
        pdf.save('relatorio-remoto.pdf')
        //document.getElementById('pdf').innerHTML = ''
      })
    },
    onClick() {
      this.alaNo = this.alaNo + 1
      var ComponentClass = Vue.extend(Button)
      var instance = new ComponentClass({
        propsData: {alanNo: this.alaNo, arttir: 'Arttır', azalt: 'Azalt' }
      })
      instance.$slots.default = ['Alan No: ' + this.alaNo]
      instance.$on('data', (e) => {
        this.gelen = e.alanNo +'=>'+ e.left+'-'+e.top
        if (this.alnLst.length === 0){
          this.alnLst.push({alanNo:e.alanNo, left:e.left, top:e.top})
        }
        let yeni = 0;
        this.alnLst.forEach(function (i) {
          if (i.alanNo === e.alanNo) {
            i.alanNo = e.alanNo;
            i.left = e.left;
            i.top = e.top;
            yeni = 1;
          }else {
            return true;
          }
        });
        if (yeni === 0) {
          this.alnLst.push({alanNo:e.alanNo, left:e.left, top:e.top});
        }
      })
      instance.$mount()
      this.$refs.container.appendChild(instance.$el)
    }
  },
  computed: {

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
