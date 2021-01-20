<template>
  <div id="test">
    <div class="row">
      <div class="col-1"><i class="fa fa-frown-o fa-lg" aria-hidden="true"></i></div>
      <div class="col-6">
        <vue-slider v-model="value" :marks="marks" :process="process2" height="10px" v-bind="options"
        @change="SliderColors(value)" :tooltip-formatter="tooltipLabel(value)">
          <template v-slot:label="{ label, active }">
            <div :class="['vue-slider-mark-label', 'custom-label', { active }]">{{ label }}%</div>
          </template>
        </vue-slider>
      </div>
      <div class="col-1"><i class="fa fa-smile-o fa-lg" aria-hidden="true"></i></div>
      <div class="col-4 align-justify">
        <v-popover offset="16" :disabled="!isEnabled">
        <i class="fa fa-info-circle fa-lg cursor-pointer" aria-hidden="true"></i>
        <template slot="popover">
          <p>
            <LikertTableTest/>
          </p>
          <a v-close-popover><i class="fa fa-window-close fa-lg cursor-pointer" aria-hidden="true"></i></a>
        </template>
      </v-popover>
      </div>
    </div>
    <div class="row" style="padding-top: 30px;">
      <div class="col-12 align-justify">
        <span style="padding-left: inherit;font-size: large;">
          {{tooltipLabel(value)}}
        </span>
      </div>
    </div>
  </div>
</template>

<style>
  @import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css");
  @import "~bootstrap/dist/css/bootstrap.css";
  @import "~bootstrap-vue/dist/bootstrap-vue.css";
  
  .tooltip {
    display: block !important;
    z-index: 10000;
  }

  .tooltip .tooltip-inner {
    background: black;
    color: #f9f9f9;
    border-radius: 16px;
    padding: 5px 10px 4px;
  }

  .tooltip .tooltip-arrow {
    width: 0;
    height: 0;
    border-style: solid;
    position: absolute;
    margin: 5px;
    border-color: black;
    z-index: 1;
  }

  .tooltip[x-placement^="top"] {
    margin-bottom: 5px;
  }

  .tooltip[x-placement^="top"] .tooltip-arrow {
    border-width: 5px 5px 0 5px;
    border-left-color: transparent !important;
    border-right-color: transparent !important;
    border-bottom-color: transparent !important;
    bottom: -5px;
    left: calc(50% - 5px);
    margin-top: 0;
    margin-bottom: 0;
  }

  .tooltip[x-placement^="bottom"] {
    margin-top: 5px;
  }

  .tooltip[x-placement^="bottom"] .tooltip-arrow {
    border-width: 0 5px 5px 5px;
    border-left-color: transparent !important;
    border-right-color: transparent !important;
    border-top-color: transparent !important;
    top: -5px;
    left: calc(50% - 5px);
    margin-top: 0;
    margin-bottom: 0;
  }

  .tooltip[x-placement^="right"] {
    margin-left: 5px;
  }

  .tooltip[x-placement^="right"] .tooltip-arrow {
    border-width: 5px 5px 5px 0;
    border-left-color: transparent !important;
    border-top-color: transparent !important;
    border-bottom-color: transparent !important;
    left: -5px;
    top: calc(50% - 5px);
    margin-left: 0;
    margin-right: 0;
  }

  .tooltip[x-placement^="left"] {
    margin-right: 5px;
  }

  .tooltip[x-placement^="left"] .tooltip-arrow {
    border-width: 5px 0 5px 5px;
    border-top-color: transparent !important;
    border-right-color: transparent !important;
    border-bottom-color: transparent !important;
    right: -5px;
    top: calc(50% - 5px);
    margin-left: 0;
    margin-right: 0;
  }

  .tooltip.popover .popover-inner {
    background:#a7d9bb;
    color: black;
    padding: 10px;
    border-radius: 5px;
    box-shadow: 0 5px 30px rgba(black, .1);
  }

  .tooltip.popover .popover-arrow {
    border-color: #f9f9f9;
  }

  .tooltip[aria-hidden='true'] {
    visibility: hidden;
    opacity: 0;
    transition: opacity .15s, visibility .15s;
  }

  .tooltip[aria-hidden='false'] {
    visibility: visible;
    opacity: 1;
    transition: opacity .15s;
  }

  .cursor-pointer {
    cursor: pointer !important;
  }

  .align-justify {
    text-align: justify;
  }
</style>

<script>
import Vue from 'vue'
import VueSlider from 'vue-slider-component';
import { VTooltip, VPopover, VClosePopover } from 'v-tooltip'
import 'vue-slider-component/theme/antd.css'
import constant from "../utils/constants";
import LikertTableTest from '../components/LikertTableTest'

Vue.directive('tooltip', VTooltip)
Vue.directive('close-popover', VClosePopover)
Vue.component('v-popover', VPopover)

export default {
  name: "SliderTest",
  components: {
    VueSlider,
    LikertTableTest
  },
  computed: {
    SliderColors() {
      return value => {
        this.dotsPos = []
        switch(true) {
          case (value < 20 && value >= 0): 
            this.process2 = dotsPos => [
            [0, value, { backgroundColor: constant.BgColor.first.color }]]
            break

          case (value <= 40 && value >= 20): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, value, { backgroundColor: constant.BgColor.second.color }]]
            break

          case (value <= 60 && value >= 40): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, value, { backgroundColor: constant.BgColor.third.color }]]
            break

          case (value <= 80 && value >= 60): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, 60, { backgroundColor: constant.BgColor.third.color }],
            [60, value, { backgroundColor: constant.BgColor.fourth.color }]]
            break
          
          case (value <= 100 && value >= 80): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, 60, { backgroundColor: constant.BgColor.third.color }],
            [60, 80, { backgroundColor: constant.BgColor.fourth.color }],
            [80, value, { backgroundColor: constant.BgColor.fifth.color }]]
            break 
        }
      }
    },
    tooltipLabel() {
      return value => {
        let label = ''
        switch(true) {
          case (value < 20 && value >= 0): 
            label = `To a very small extent: ${value}%`
            break

          case (value <= 40 && value >= 20): 
            label = `To a small extent: ${value}%`
            break

          case (value <= 60 && value >= 40): 
            label = `Somewhat: ${value}%`
            break

          case (value <= 80 && value >= 60): 
            label = `To a great extent: ${value}%`
            break
          
          case (value <= 100 && value >= 80): 
            label = `To a very great extent: ${value}%`
            break 
        }
        return label
      }
    }
  },
  data () {
    return {
      value: [0],
      marks: val => val % (100/5) === 0,
      process2: dotsPos => [],
      isEnabled: true,
      msg: 'test',
      dotsPos: [],
      options: {
        dotSize: 14,
        width: 'auto',
        height: 4,
        contained: false,
        direction: 'ltr',
        data: null,
        dataLabel: 'label',
        dataValue: 'value',
        min: 0,
        max: 100,
        interval: 1,
        disabled: false,
        clickable: true,
        duration: 0.5,
        adsorb: false,
        lazy: false,
        tooltip: 'active',
        tooltipPlacement: 'top',
        tooltipFormatter: void 0,
        useKeyboard: false,
        keydownHook: null,
        dragOnClick: false,
        enableCross: true,
        fixed: false,
        minRange: void 0,
        maxRange: void 0,
        order: true,
        marks: false,
        dotOptions: void 0,
        dotAttrs: void 0,
        process: true,
        dotStyle: void 0,
        railStyle: void 0,
        processStyle: void 0,
        tooltipStyle: void 0,
        stepStyle: void 0,
        stepActiveStyle: void 0,
        labelStyle: void 0,
        labelActiveStyle: void 0,
      }
    }
  }
}
</script>