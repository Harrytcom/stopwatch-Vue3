<template>
  <div>
    <Stopwatches>
      <Stopwatch />
    </Stopwatches>
  </div>
</template>
<script>
import Stopwatches from './Stopwatches.vue';
import Stopwatch from './Stopwatch.vue';

export default {
    components: { 
      Stopwatches,
      Stopwatch
    }
}
</script>
<style>
  
</style>