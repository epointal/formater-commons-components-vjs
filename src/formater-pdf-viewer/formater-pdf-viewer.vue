<template>
   <div class="formater-container">

		
		<input v-model.number="page" type="number" style="width: 5em"> /{{numPages}}
		<button @click="rotate += 90">&#x27F3;</button>
		<button @click="rotate -= 90">&#x27F2;</button>
		<button @click="$refs.pdf.print()">print</button>
		<a :href="src" download><i class="fa fa-download"></i></a>
		<div style="width: 50%">
			<div v-if="loadedRatio > 0 && loadedRatio < 1" style="background-color: green; color: white; text-align: center" :style="{ width: loadedRatio * 100 + '%' }">{{ Math.floor(loadedRatio * 100) }}%</div>
			<pdf  ref="pdf" class="formater-vue-pdf" :src="src" :page="page" :rotate="rotate" @progress="loadedRatio = $event" @error="error" @numPages="numPages = $event"></pdf>
		</div>
	</div>
</template>

<script>

import pdf from 'vue-pdf';

export default {
  components: {
        pdf
      },
  props:{
      src: {
          type: String
      }
  },
  data () {
		return {
  			show: true,
			loadedRatio: 0,
			page: 1,
			numPages: 0,
			rotate: 0
		}
  },
  methods: {
		error: function(err) {

			console.log(err);
		}
	}
}
</script>
<style>
.formater-container a{
   color: black;
}
.formater-vue-pdf{
   border:1px solid black;
}
</style>