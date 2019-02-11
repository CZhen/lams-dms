<template style="height:100%">
  <view-box ref="viewBox">
    <deviceitem v-for="device in devices" :device="device" :key="device.id">
    </deviceitem>
  </view-box>
</template>

<script>
import { ViewBox } from 'vux'
import DeviceItem from './DeviceItem'

export default {
  components: {
    ViewBox,
    'deviceitem': DeviceItem
  },
  methods: {
    formatDevice (device) {
      return {
        title: device.name,
        desc: device.description,
        src: device.images
      }
    }
  },
  mounted () {
    this.axios
      .get('http://api.lams.com/devices')
      .then(response => {
        this.devices = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally()
  },
  data () {
    return {
      devices: []
    }
  }
}
</script>

<style>
html, body {
  height: 100%;
  width: 100%;
  overflow-x: hidden;
}
</style>
