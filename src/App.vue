<template>
  <div id="app">
    <pre>Sel: {{ sel }}</pre>
    <accordion-list v-model="sel">
      <accordion v-for="d in data" :duration="500" :key="d" class="item">
        <template #header class="ziax">
          <div class="pad header">
            header {{ d }}
          </div>
        </template>
        <template #body>
          <div class="pad body">
            body {{ d }}
          </div>
        </template>
      </accordion>

    </accordion-list>
    <hr/>
    <pre>Sel2: {{ sel2 }}</pre>
    <accordion-list v-model="sel2">
      <accordion v-for="d in data2" :duration="500" :key="d.a" :value="d" class="item">
        <template #header>
          <div class="pad header">
            header {{ d.a }}
          </div>
        </template>
        <template #body>
          <div class="pad body">
            body {{ d }}
          </div>
        </template>
      </accordion>

    </accordion-list>
  </div>
</template>

<script>
import AccordionList from './Accordion-list.vue'
import Accordion from './Accordion.vue'

const dataObj = [{ a: 1 }, { a: 2 }, { a: 3 }]

export default {
  name: 'app',
  data () {
    return {
      data: [1, 2, 3, 4, 5],
      sel: 3
      ,
      data2: dataObj,
      sel2: dataObj[1]


    }
  },
  components: {
    AccordionList,
    Accordion
  }
}
</script>

<style scoped>
.pad {
  padding: 4px;
}
.header {
  cursor: pointer;
}
.body {
  font-size: 22px;
  background-color: beige;
}
.item {
  border: 1px solid blacK;
}
</style>
