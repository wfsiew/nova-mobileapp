<script setup lang="ts">
import { ref, onMounted } from 'vue'
import QrcodeVue from 'qrcode.vue'

// const level = ref<Level>('M')
// const renderAs = ref<RenderAs>('svg')

const apps = ref([
  { ver: '', name: 'CVSKLgo UAT', nd: 'https://app.box.com/s/zi7ir5h5qm3fxk6nak7sfmx67ov9w9xc', ios: 'https://testflight.apple.com/join/0WgSF7EN' },
  { ver: '', name: 'Vesalius Patient Nova', nd: 'https://app.box.com/s/6avwv24c120wqgyfdcmfudsr56ledb77', ios: 'https://testflight.apple.com/join/Z51JPUlX' },
  { ver: '...', name: 'Vesalius Patient IH', nd: 'https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/ihp', ios: 'https://testflight.apple.com/join/PKfbGUal' },
  { ver: '...', name: 'Vesalius Patient IH UAT', nd: 'https://202.73.42.183:43901/mobile_central_2_0_0/files/uat/ihp', ios: 'https://testflight.apple.com/join/yTzICG9R' },
  { ver: '...', name: 'SkAi Lite UAT', nd: 'https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-lite', ios: 'https://testflight.apple.com/join/0PsM6mCs' },
  { ver: '...', name: 'SkAi CT UAT', nd: 'https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-ct', ios: 'https://testflight.apple.com/join/6Xv7RLjl' },
  { ver: '', name: 'SkAi Pro UAT', nd: 'https://testflight.apple.com/join/yOud71n7', ios: 'https://testflight.apple.com/join/yOud71n7' },
  { ver: '...', name: 'SkAi Pro CT UAT', nd: 'https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-pro-ct', ios: 'https://testflight.apple.com/join/345Gey6K' }
])

onMounted(async () => {
  const devih = await fetch('https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/ihp/ver')
  const uatih = await fetch('https://202.73.42.183:43901/mobile_central_2_0_0/files/uat/ihp/ver')
  const skailite = await fetch('https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-lite/ver')
  const skaict = await fetch('https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-ct/ver')
  const skaiproct = await fetch('https://202.73.42.183:43901/mobile_central_2_0_0/files/dev/skai-pro-ct/ver')
  apps.value[2].ver = await devih.text()
  apps.value[3].ver = await uatih.text()
  apps.value[4].ver = await skailite.text()
  apps.value[5].ver = await skaict.text()
  apps.value[7].ver = await skaiproct.text()
})
</script>

<template>
  <div class="album py-2 bg-light">
    <div class="container py-2">
      <template v-for="app in apps" :key="app.name">
        <div class="row">
          <div class="col-12 h3">{{ app.name }}</div>
        </div>
        <div class="row pb-4">
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12">
            <div class="card shadow-sm p-2">
              <div class="card-body">
                <div class="d-flex align-items-center justify-content-center rounded text-center col-12">
                  <qrcode-vue :value="app.nd" :size="225" />
                </div>
                <div class="col-12 d-flex align-items-center justify-content-center pt-2">
                  <i class="bi bi-android h1"></i>
                  <template v-if="app.ver">
                    &nbsp;<span class="h5">{{ app.ver }}</span>
                  </template>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-6 col-lg-6 col-md-6 col-sm-12">
            <div class="card shadow-sm p-2">
              <div class="card-body">
                <div class="d-flex align-items-center justify-content-center rounded text-center col-12">
                  <qrcode-vue :value="app.ios" :size="225" />
                </div>
                <div class="col-12 d-flex align-items-center justify-content-center pt-2">
                  <i class="bi bi-apple h1"></i>
                </div>
              </div>
            </div>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<style scoped>

</style>
