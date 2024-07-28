<template>
  <FabCanvas></FabCanvas>
</template>

<script>
import FabCanvas from '@/components/FabricCanvas.vue'

export default {
  name: 'Draw',
  data() {
    return {
      showDialog: false,
    }
  },
  resources: {
    ping: {
      url: 'ping',
    },
  },
  components: {
    FabCanvas,
  },
}
</script>
