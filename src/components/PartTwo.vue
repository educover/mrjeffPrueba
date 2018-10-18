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
   
   
    <div class="exercise">
      <h1>Ejercicio 5</h1>
      <p>Una vez tenemos los datos formateados, tenemos que mostrarlos por pantalla con el siguiente formato:</p>
      <img src="@/assets/timetable.png">

      
    </div>
{{timetableCorrect}}
{{selectDays}}
{{filtrarDatos}}
    <hr>
    
    <div v-show="muestraDatos">
      <div class="table">
      <table>
        <thead>
          <tr>
            <th scope="col" v-for="item in dataFilter" :key="item.dayOfWeek">
              <b>{{item.dayOfWeek}}</b>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr>
              <td scope="row" v-for="item in dataFilter" :key="item.dayOfWeek">
              <span class="text" v-for="it in item.timeSlotCodes" :key="it">
                {{it}}
              </span>
              </td>
              
          </tr>
        </tbody>
      </table>
      </div>
    </div>
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
      timetableLog:[],
      dataFilter:[],
      muestraDatos:false
    };
  },
  computed:{
    timetableCorrect(){
      this.timetableLog = this.timetable.filter(item=>{
        if(item.timetableType==="LOGISTICS"){
          return item;
      }
    })
      
    },
    selectDays(){
      let b = 0;
      for (let i = 0; i < this.timetable.length; i++) {
        if(this.timetable[i].timetableType==="LOGISTICS"){
           let obj= {}
            obj.dayOfWeek =  this.timetable[i].dayOfWeek;
            this.dataFilter[b] = obj;
            b++;
            obj=null;    
        }
      }
      for (let a = 0; a <  this.dataFilter.length; a++) {
         this.dataFilter[a].timeSlotCodes = new Array(); 
      }
    },
    filtrarDatos(){
      let z=0;
      for (let index = 0; index < this.timetableLog.length; index++) {
        for (let i=0 ; i < this.timetableLog[index].defaultTimetableTimeSlotConfigurations.length; i++) {
          if(this.timetableLog[index].defaultTimetableTimeSlotConfigurations[i].visitTypeCode=="PICKUP"){
            for (let b = 0; b < this.dataFilter.length; b++) {
              if(this.dataFilter[b].dayOfWeek==this.timetableLog[index].dayOfWeek){
                 this.dataFilter[b].timeSlotCodes.push(this.timetableLog[index].defaultTimetableTimeSlotConfigurations[i].timeSlotCode)
              }
            }

          }
        }
        this.dataFilter[index].timeSlotCodes.sort();
     }
     console.log(this.dataFilter)
     
      this.muestraDatos=true;
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

.table{
  border:black 1px solid;
  padding:1em;
}

tr, th{
  margin-bottom: 4em;
}

</style>