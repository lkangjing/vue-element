<template>
  <div class="amap-wrapper" :style="'max-height:450px;'">
    <div class="amap-page-container">
      <el-amap-search-box class="search-box" :search-option="searchOption" :on-search-result="onSearchResult" />
      <el-amap vid="amapDemo" :center="mapCenter" :zoom="12" class="amap-demo">
        <!-- 地图标记点 -->
        <el-amap-marker v-for="(marker,i) in markers" :key="i" :position="marker.position" :events="marker.events" />
        <!-- 信息弹窗 -->
        <el-amap-info-window
          v-if="window"
          :position="window.position"
          :visible="window.visible"
          :content="window.content"
        >
          <el-amap-info-window />
        </el-amap-info-window></el-amap>
    </div>
  </div>
</template>
<script>
module.exports = {
  data: function() {
    return {
      //   markers: [
      //     { position: [121.59996, 31.197646] },
      //     { position: [121.40018, 31.197622] },
      //     { position: [121.69991, 31.207649] }
      //   ],
      searchOption: {
        city: '上海',
        citylimit: true
      },
      mapCenter: [121.59996, 31.197646],
      windows: [],
      markers: [],
      window: ''
    }
  },
  mounted() {
    const markers = []
    const windows = []

    const num = 4
    const self = this

    for (let i = 0; i < num; i++) {
      markers.push({
        position: [121.59996, 31.197646 + i * 0.001],
        events: {
          click() {
            self.windows.forEach(window => {
              window.visible = false
            })

            self.window = self.windows[i]
            self.$nextTick(() => {
              self.window.visible = true
            })
          }
        }
      })

      windows.push({
        position: [121.59996, 31.197646 + i * 0.001],
        // content: `<div class="prompt">${i}+河南省郑州市<a>链接<a/></div>`,
        content: `<div class="prompt">
                                <span class="prompt-span"><a href="/#/company/` + i + `">` + i + `</a></span>
                                <p class="prompt-p">` + i + `</p>
                                </div>`,
        visible: false
      })
    }

    this.markers = markers
    this.windows = windows
  },
  methods: {
    handleClick() {
      console.log('点击了弹窗')
    },
    onSearchResult(pois) {
      let latSum = 0
      let lngSum = 0
      if (pois.length > 0) {
        pois.forEach(poi => {
          const { lng, lat } = poi
          lngSum += lng
          latSum += lat
          this.markers.push([poi.lng, poi.lat])
        })
        const center = {
          lng: lngSum / pois.length,
          lat: latSum / pois.length
        }
        this.mapCenter = [center.lng, center.lat]
      }
    }
  }
}
</script>
  <style lang="scss" scoped>
    .amap-demo {
      height: 300px;
    }

    .search-box {
      position: absolute;
      top: 25px;
      left: 20px;
    }

    .amap-page-container {
        margin: 50px;
        width: 50%;
      position: relative;
    }
    .prompt {
        position: relative;
        display: inline-block;
      background: white;
      width: 200px;
      height: 60px;
      text-align: center;
    }
  </style>

