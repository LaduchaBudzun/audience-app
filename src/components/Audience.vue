<template>
  <div class="hello">
  <div class="times">
    <div>
       <span>От</span>
       <select v-model="from">
            <option v-for="(tim,index) in time.slice(1,-1)" v-bind:value="tim" :key="index">{{tim.startTime}}</option>
        </select>
    </div>
       <div>
         <span>До</span>
       <select v-model="before">
            <option v-for="(tim,index) in endLesson()" v-bind:value="tim" :key="index">{{tim.startTime}}</option>
        </select>
       </div>
       
       <button @click="chooseTime" class="btn-choose">Подобрать</button>
  </div>
  <div class="table-audience">
    <table class="table_blur">
    <tr>
      <th v-for="(column,index) in time" :key="index" ><span class="time-table">{{column.startTime}}</span></th>
    </tr>

    <tr v-for="(audience,index) in audiences" :key="index">
        <td >{{audience.name}}</td>
  
       <td  class="td" v-for="(cell,index) in time.slice(1)" :key="index" >
          <draggable group="todosapp" :list="audience.events" > 
        <div :list="meeting" :style="{width: widthMeeting(meeting) }" v-for="(meeting,index) in audience.events" :key="index" class="meeting-item">{{displayMeeting(meeting, cell)}}</div>
       </draggable>
       </td>
  
      </tr>
    
  
  </table>
  
  </div>

  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  components:{
    draggable
  },
  name: 'Audience',
  data(){
    return{
      user:'',
      from:{startTime:"8:00",id:1},
      before:'',
      time:[
        {},
        {startTime:"8:00",id:1},
        {startTime:"8:30",id:2},
        {startTime:"9:00",id:3},
        {startTime:"9:30",id:4},
        {startTime:"10:00",id:5},
        {startTime:"10:30",id:6},
        {startTime:"11:00",id:7},
        {startTime:"11:30",id:8},
        {startTime:"12:00",id:9},
        {startTime:"12:30",id:10},
        {startTime:"13:00",id:11},
        {startTime:"13:30",id:12},
        {startTime:"14:00",id:13},
        {startTime:"14:30",id:14},
        {startTime:"15:00",id:15},
        {startTime:"15:30",id:16},
        {startTime:"16:00",id:17},
        {startTime:"16:30",id:18},
        {startTime:"17:00",id:19},
        {startTime:"17:30",id:20},
        {startTime:"18:00",id:21},
      ],
      audiences:[
        {name:"Аудитория 1",
        id:1,
         events: [
          {
            name: "Совещание 1",
            start: "9:00",
            startId: 3,
            end: "11:30",
            endId: 8
          }
      ]},
        {name:"Аудитория 2",id:2,events: []},
        {name:"Аудитория 3",id:3,events: []},
        {name:"Аудитория 4",id:4,events: []},
      ]
    }
  },
  methods:{
      meetingNumber(audience){
          if(audience.events.length == 0){
            return 1
          }else{
            const arrEvents = audience.events
            const num = Number(arrEvents[arrEvents.length - 1].name.split(" ")[1]) + 1
            return num
          }
             
          },
      chooseTime(){
          let start = this.from
          let end = this.before
          if(start == "" || end == ""){
            alert("Выберите время")
            return
          }
          
          this.audiences.every(audience =>{

            const evenStart = (element) => start.id >= element.startId && start.id < element.endId 
            const evenEnd = (element) => end.id > element.startId && end.id <= element.endId 
            const evenStartBetween = (element) => element.startId >= start.id && element.startId < end.id
            

              if(audience.events.some(evenStart)){
                return true
              }else if(audience.events.some(evenEnd)){
                return true
              }else if(audience.events.some(evenStartBetween)){
                return true
              }else {
                  
                audience.events.push({
                  
                      name: `Совещание ${this.meetingNumber(audience)}`,
                      start: `${start.startTime}`,
                      startId: start.id,
                      end: `${end.startTime}`,
                      endId: end.id
                  })
                  alert(`Запись в ${audience.id} аудиторию`)
                 return false   
              }
            
          

          })
      },
      startLesson(){
        
           return this.time.slice((this.from.id))
          
        },
      endLesson(){
        
           return this.time.slice((this.from.id + 1))
          
        },
      //  displayEvents(audience,cell) {

      //    const even = (element) => cell.id >= element.startId && cell.id < element.endId 
         

      //    if (audience.events.some(even)){
      //     return true
      //    }
      //  },
       displayMeeting(meeting, cell) {
            
          if(cell.id == meeting.startId ){
               return meeting.name
             }  
          
       },
       widthMeeting(meeting){
         let width = meeting.endId - meeting.startId
          if(width > 1){
            width = width*50
          } else {
            width = 50
          }
          console.log(`${width}px`)
          return `${width}px`
       }
    
      }
  }
  

</script>


<style scoped>
.on-drag{
  color: #fff;
  background-color: rgb(103,174,255);
  z-index: 10;
  border: none;
}
.td{

  
}
.meeting-item{
  font-size: 8px;
  position: absolute;
  background-color: royalblue;
  color: white;
  line-height: 50px;
  
  left: 0;
  top: 0;
  z-index: 10;
  border-radius: 10px;
  cursor: move;
}
.btn-choose{
  background-color: #5a567f;
  color: #f6fbff;
  border-radius: 5px;
}
.times{
  display: flex;
  justify-content: center;
  gap: 30px;
  margin-bottom: 10px;
}
.times span{
  margin-right: 5px;
}
.table-audience{
  display: flex;
  justify-content: center;
}
.time-table{
    position: relative;
    left: -21px;
}
/*table */
.table_blur {
  background: #f5ffff;
  border-collapse: collapse;
  text-align: left;
}
.table_blur th {
  border-top: 1px solid #777777;	
  border-bottom: 1px solid #777777; 
  box-shadow: inset 0 1px 0 #999999, inset 0 -1px 0 #999999;
  background: linear-gradient(#9595b6, #5a567f);
  color: white;
  padding: 4px 8px;
  position: relative;
  font-size: 12px;
}
.table_blur th:after {
  content: "";
  display: block;
  position: absolute;
  left: 0;
  top: 25%;
  height: 25%;
  width: 100%;
  background: linear-gradient(rgba(255, 255, 255, 0), rgba(255,255,255,.08));
}
.table_blur tr:nth-child(odd) {
  background: #ebf3f9;
}
.table_blur th:first-child {
  border-left: 1px solid #777777;	
  border-bottom:  1px solid #777777;
  box-shadow: inset 1px 1px 0 #999999, inset 0 -1px 0 #999999;
}
.table_blur th:last-child {
  border-right: 1px solid #777777;
  border-bottom:  1px solid #777777;
  box-shadow: inset -1px 1px 0 #999999, inset 0 -1px 0 #999999;
}
.table_blur td {
  border: 1px solid #e3eef7;
  
  position: relative;
  transition: all 0.5s ease;
  text-align: center;
  width: 50px;
  height: 50px;
}
.table_blur tbody:hover td {
  color: transparent;
  text-shadow: 0 0 3px #a09f9d;
}
.table_blur tbody:hover tr:hover td {
  color: #444444;
  text-shadow: none;
}
</style>
