<template>
  <div class="part">
    <hr>
    <div class="exercise">
      <h1>Ejercicio 3</h1>
      <p>
        Implementa una llamada HTTP con la librería <code>Axios</code> para llamar a un servicio de la API de MrJeff
        <a href="https://github.com/axios/axios" target="_blank" rel="noopener noreferrer">( Documentación de Axios )</a>
        Haz uso del botón de abajo para que realize la llamada al clickar.
      </p>
      <p>
        <strong>URL: </strong>
        <code>
          https://dev.backoffice.v1.backend.mrjeffapp.net/timetable-service/v1/defaultTimetableConfigurations
        </code>
      </p>
      <p><strong>Params: </strong><code>countryCode: ES</code></p>
      <p><strong>Token: </strong></p>
      <textarea rows=8 style="width: 100%">eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqdWFuZGllZ29AbXJqZWZmYXBwLmNvbSIsInJvbGVzIjpbIlJPTEVfQkFDS09GRklDRSJdLCJuYW1lIjoiSnVhbiBEaWVnbyIsImlzcyI6ImJhY2tvZmZpY2UubXJqZWZmYXBwLm5ldCIsImlkIjoiOGM3OWI3NjctNWJjZS00Y2NmLTk1NmUtMDZmMWJmOWJkMTkwIiwiZnVsbG5hbWUiOiJKdWFuIERpZWdvIC4iLCJ0eXBlIjoidXNlciIsImV4cCI6MTU0MDE5MDc0NCwiaWF0IjoxNTM5NTg1OTQ0LCJqdGkiOiIxMTU1YjRlOC1lMzI2LTRhM2QtOWI0Mi1mZDU0MTYxYzVlOWMiLCJlbWFpbCI6Imp1YW5kaWVnb0BtcmplZmZhcHAuY29tIn0.edbZq_FoscsNVRAxx__iAtNwahQld1UNw120ZHm8_lolWDqgwGuAore4OVlli-MCuO2MwD_xk5jy9P4QdzpAWg
      </textarea>
      <!-- <p><strong>Token: </strong><code>eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqdWFuZGllZ29AbXJqZWZmYXBwLmNvbSIsInJvbGVzIjpbIlJPTEVfQkFDS09GRklDRSJdLCJuYW1lIjoiSnVhbiBEaWVnbyIsImlzcyI6ImJhY2tvZmZpY2UubXJqZWZmYXBwLm5ldCIsImlkIjoiOGM3OWI3NjctNWJjZS00Y2NmLTk1NmUtMDZmMWJmOWJkMTkwIiwiZnVsbG5hbWUiOiJKdWFuIERpZWdvIC4iLCJ0eXBlIjoidXNlciIsImV4cCI6MTU0MDE5MDc0NCwiaWF0IjoxNTM5NTg1OTQ0LCJqdGkiOiIxMTU1YjRlOC1lMzI2LTRhM2QtOWI0Mi1mZDU0MTYxYzVlOWMiLCJlbWFpbCI6Imp1YW5kaWVnb0BtcmplZmZhcHAuY29tIn0.edbZq_FoscsNVRAxx__iAtNwahQld1UNw120ZHm8_lolWDqgwGuAore4OVlli-MCuO2MwD_xk5jy9P4QdzpAWg</code></p> -->
      <button @click="request" class="request-button">Hacer Llamada</button>
    </div>

    <hr>
    
    <div class="exercise">
      <h1>Ejercicio 4</h1>
      <p>Con los datos obtenidos en la anterior llamada, extrae los dias que tengan como <code>timetableType: "LOGISTICS"</code> y los horarios que tengan como <code>visitTypeCode: "PICKUP"</code> y conviertelos al siguiente formato:</p>
      <div class="code">
        [
        <br>
        &nbsp;&nbsp;&nbsp;{
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dayOfWeek: 'MONDAY',
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;timeSlotCodes:
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'10:00-11:00',
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'11:00-12:00',
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'12:00-13:00',
        <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]
        <br>
        &nbsp;&nbsp;&nbsp;},
        <br>
        &nbsp;&nbsp;&nbsp;{...},
        <br>
        &nbsp;&nbsp;&nbsp;{...},
        <br>
        &nbsp;&nbsp;&nbsp;{...}
        <br>
        ]
      </div>

    </div>
    
    <hr>
    {{timetableCorrect}}
   {{otraComputed}}
    <div class="exercise">
      <h1>Ejercicio 5</h1>
      <p>Una vez tenemos los datos formateados, tenemos que mostrarlos por pantalla con el siguiente formato:</p>
      <img src="@/assets/timetable.png">

      
    </div>

    <hr>
    
  
  <button @click="otraComputed">filtrar 2 vez</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PartTwo",

  methods: {
    request() {
      const TOKEN =
        "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqdWFuZGllZ29AbXJqZWZmYXBwLmNvbSIsInJvbGVzIjpbIlJPTEVfQkFDS09GRklDRSJdLCJuYW1lIjoianVhbiBkaWVnbyIsImlzcyI6ImJhY2tvZmZpY2UubXJqZWZmYXBwLm5ldCIsImlkIjoiYWEwNDdhNDAtNGM1Yi00ZjZjLWEwNTktMmQwMjFmY2UxYWMxIiwiZnVsbG5hbWUiOiJqdWFuIGRpZWdvIGFwZWxsIiwidHlwZSI6InVzZXIiLCJleHAiOjE1NDAwMzQ2OTUsImlhdCI6MTUzOTQyOTg5NSwianRpIjoiNzcyM2Y3NDgtN2Y4Mi00NzNlLTg5NTctMDI2YjEwYzlmMDg0IiwiZW1haWwiOiJqdWFuZGllZ29AbXJqZWZmYXBwLmNvbSJ9.BMAYtAERPWP5Fw7eR-qB53_aO5o0Eo9smArh9BZ0xLwz6kiJgVe68EESK74X6YXHwxkMXfZyS8e61D8Q4R8VaA";
      let config = {
        headers: {
          Authorization: "Bearer " + TOKEN
        },
        params: {
          countryCode: "ES"
        }
      };
      axios
        .get(
          "https://dev.backoffice.v1.backend.mrjeffapp.net/timetable-service/v1/defaultTimetableConfigurations",
        
          config
          
        )
        .then(response => {
          this.timetable = response.data;
         
        })
        .catch(error => {
          console.log(error);
        });
    },
  },

  data() {
    return {
      timetable: [],
      timeType:[],
      visitCode:[]
    };
  },
  computed:{
    timetableCorrect(){
      this.timeType = this.timetable.filter(day=>{
            if(day.timetableType==="LOGISTICS"){
                return day;
            }
          })
    },
    otraComputed(){
      let a;
      let i;
      for (let index = 0; index < this.timeType.length; index++) {
        a=0;
        i=0;
        console.log('----------------------------- iteracion-->'+index)
        for ( i ; i < this.timeType[index].defaultTimetableTimeSlotConfigurations.length; i++) {
          
          if(this.timeType[index].defaultTimetableTimeSlotConfigurations[i].visitTypeCode==="PICKUP"){
             console.log('PICKUP-----------' + this.timeType[index].defaultTimetableTimeSlotConfigurations[i].visitTypeCode + i);
           
            
          }else{
            console.log('DELIVERY----------'+this.timeType[index].defaultTimetableTimeSlotConfigurations[i].visitTypeCode + i);
            
            //console.log(this.timeType[index].defaultTimetableTimeSlotConfigurations[i])
             this.timeType[index].defaultTimetableTimeSlotConfigurations.splice(i, 1);
             i--;
             //console.log(this.timeType[index].defaultTimetableTimeSlotConfigurations[i-a])
            
            
          }
          
        }
         }
    }
    
  }
};
</script>

<style>
.part {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  width: 75vw;
}
p {
  text-align: left;
  margin: 0.5rem 0;
}
textarea {
  margin-bottom: 1rem;
}
img {
  width: 100%;
  border: 1px solid black;
  margin-top: 1rem;
}
code {
  padding: 0.2rem 1rem;
  background-color: rgb(225, 225, 225);
  border-radius: 4px;
}
.request-button {
  font-size: 2rem;
  background-color: transparent;
  border-radius: 4px;
  padding: 0.5rem 1rem;
  transition: all 0.2s;
}
.request-button:hover {
  background-color: rgb(225, 225, 225);
  transform: translateY(-4px);
}
.code {
  text-align: left;
  font-family: monospace;
  background-color: rgb(225, 225, 225);
  padding: 1rem;
  border-radius: 4px;
  margin: 1rem auto;
  width: fit-content;
}
</style>