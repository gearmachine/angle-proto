<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="12" md="12">
      <svg version="1.1"
        baseProfile="full"
        :width="width" :height="height"
        xmlns="http://www.w3.org/2000/svg">
        <g fill="none" stroke="black" stroke-width="2" :transform="transform">
          <line :x1="x1" :y1="y1" :x2="x2" :y2="y2" />
          <circle :cx="x1" :cy="y1" r="10" />
          <!--<path :d="arc"/>-->
        </g>
      </svg>
      {{angles[index] +', '+ calcAngle(angles[index])}}
      <v-btn @click="changeAngle">更新</v-btn>
    </v-col>
  </v-row>
</template>

<script>
//import Logo from '~/components/Logo.vue'
//import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
  },
  data() {
    return {
      width: 800,
      height: 600,
      r: 50,
      x1: 800/2 ,
      y1: 0,
      x2: 800/2,
      y2: 600/2,
      angle: 0,
      angles: [
        '00:00', '00:15', '00:30', '00:45', 
        '01:00', '01:15', '01:30', '01:45', 
        '02:00', '02:15', '02:30', '02:45', 
        '03:00', '03:15', '03:30', '03:45', 
        '04:00', '04:15', '04:30', '04:45', 
        '05:00', '05:15', '05:30', '05:45', 
      ],
      index: 0
    }
  },
  mounted() {
    this.changeAngle();
  },
  computed: {
    transform() {
      return "translate(0,"+this.r+") rotate(" + this.calcAngle(this.angles[this.index]) + ", 400, 150)"
    },
    arc() {
      let angle = this.calcAngle(this.angles[this.index]);
      let r = this.r;
      let sx = this.x2; 
      let sy = this.y2 - r; 
      let ex = sx - r * Math.sin(angle/180 * Math.PI);
      let ey = this.y2 - r * Math.cos(angle/180 * Math.PI);
      console.log('angle:', angle, ', sx:',sx, ', sy:', sy, ', ex:', ex, ', ey:', ey);
      return "M "+sx+","+sy+" A "+r+" "+r+" 0 0 0 "+ex+","+ey;
    }

  },
  methods: {
    calcAngle(timeStr) {
      let [h, m] = timeStr.split(':');
      let angle = parseInt(h) * 360/12 + parseInt(m) * 360/60/12;
      return angle;
    },
    changeAngle() {
      this.index = Math.floor(Math.random() * this.angles.length);
    }
  }
}
</script>
