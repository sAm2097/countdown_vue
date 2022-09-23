<template>
  <div class="home">
   <counter-file
   :year='2022'
   :month='9'
   :date='25'
   :hour='10'
   :minutes='10'
   :seconds='10'
   :milliseconds='10'>
   </counter-file>
  </div>

</template>

<script>
// @ is an alias to /src

import CounterFile from '@/components/CounterFile.vue'

export default {
  
  components: {
    CounterFile
    
  }
}
</script>
