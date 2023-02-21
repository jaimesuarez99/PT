<template>
  <main>
    <button @click="scheduleService()">Iniciar</button>
  </main>
</template>


<script setup>
import keepersDb from '../src/keepersDb'
import { reactive, ref } from 'vue';
const inputDate = {
  "id": "11ab5a01-5bec-4752-a068-1bf87963ec64",
  "date_program": "2023-01-08T08:00:00.000",
  "duration": 3
}
const serviceDate = reactive({
  starDate: '',
  endDate: '',

})
const getServiceDates = () => {

  serviceDate.starDate =  new Date(inputDate.date_program)
  serviceDate.endDate = new Date(inputDate.date_program)
  serviceDate.endDate.setHours(serviceDate.endDate.getHours()+ Number(inputDate.duration))
}

const scheduleService = () =>{
  getServiceDates()
  let scheduleKey =  []
  keepersDb.forEach(function(obj, index){
    for (const object in obj.schedule) {
      let dayDate = inputDate.date_program.split('T')
      if(object == dayDate[0]){
        scheduleKey.push({
          id: obj.id,
          shcedueDate: object
        })
      }
    }
    
  })
  console.log(scheduleKey)
}


console.log(keepersDb)

</script>

<style scoped>
main{
  display: flex;
  justify-content: center;
  align-items: center;
}


</style>
