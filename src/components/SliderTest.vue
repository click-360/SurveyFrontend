<template>
  <div id="test">
    <!-- :marks="marks" -->
    <vue-slider v-model="value" :marks="marks" :process="process2" height="10px" width="720px" v-bind="options"
    @dragging="SliderColors(value)" :tooltip-formatter="tooltipLabel(value)">
    </vue-slider>
  </div>
</template>

<script>
import VueSlider from 'vue-slider-component';
import 'vue-slider-component/theme/antd.css'
import constant from "../utils/constants";

export default {
  name: "SliderTest",
  components: {
    VueSlider
  },
  computed: {
    SliderColors() {
      return value => {
        this.dotsPos = []
        switch(true) {
          case (value < 20 && value >= 0): 
            this.process2 = dotsPos => [
              [0, value, { backgroundColor: constant.BgColor.first.color }]
            ]
            break

          case (value <= 40 && value >= 20): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, value, { backgroundColor: constant.BgColor.second.color }]
            ]
            break

          case (value <= 60 && value >= 40): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, value, { backgroundColor: constant.BgColor.third.color }]
            ]
            break

          case (value <= 80 && value >= 60): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, 60, { backgroundColor: constant.BgColor.third.color }],
            [60, value, { backgroundColor: constant.BgColor.fourth.color }]
            ]
            break
          
          case (value <= 100 && value >= 80): 
            this.process2 = dotsPos => [
            [0, 20, { backgroundColor: constant.BgColor.first.color }], 
            [20, 40, { backgroundColor: constant.BgColor.second.color }], 
            [40, 60, { backgroundColor: constant.BgColor.third.color }],
            [60, 80, { backgroundColor: constant.BgColor.fourth.color }],
            [80, value, { backgroundColor: constant.BgColor.fifth.color }]
            ]
            break 
        }
      }
    },
    tooltipLabel() {
      return value => {
        let label = ''
        switch(true) {
          case (value < 20 && value >= 0): 
            label = `${value} above 0`
            break

          case (value <= 40 && value >= 20): 
            label = `${value} above 20`
            break

          case (value <= 60 && value >= 40): 
            label = `${value} above 40`
            break

          case (value <= 80 && value >= 60): 
            label = `${value} above 60`
            break
          
          case (value <= 100 && value >= 80): 
            label = `${value} above 80`
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
      process2: dotsPos => [
      ],
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