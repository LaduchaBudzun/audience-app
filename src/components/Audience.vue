<template>
  <div class="hello">
  <div class="times">
    <div>
       <span>От</span>
       <select v-model="from">
            <option v-for="(tim,index) in time.slice(1)" v-bind:value="tim" :key="index">{{tim.start}}</option>
        </select>
    </div>
       <div>
         <span>До</span>
       <select v-model="before">
            <option v-for="(tim,index) in endLesson()" v-bind:value="tim" :key="index">{{tim.start}}</option>
        </select>
       </div>
       
       <button @click="chooseTime" class="btn-choose">Подобрать</button>
  </div>
  <div class="table-audience">
    <table class="table_blur">
    <tr>
      <th v-for="(column,index) in time" :key="index" ><span class="time-table">{{column.start}}</span></th>
    </tr>

    <tr v-for="(audience,index) in audiences" :key="index">
      <td >{{audience.name}}</td>

   <td v-for="(cell,index) in time.slice(0, -1)" :key="index" >

   </td>
 
      </tr>
    
  
  </table>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Audience',
  data(){
    return{
      user:'',
      from:{start:"8:00",id:1},
      before:'',
      time:[
        {},
        {start:"8:00",id:1},
        {start:"8:30",id:2},
        {start:"9:00",id:3},
        {start:"9:30",id:4},
        {start:"10:00",id:5},
        {start:"10:30",id:6},
        {start:"11:00",id:7},
        {start:"11:30",id:8},
        {start:"12:00",id:9},
        {start:"12:30",id:10},
        {start:"13:00",id:11},
        {start:"13:30",id:12},
        {start:"14:00",id:13},
        {start:"14:30",id:14},
        {start:"15:00",id:15},
        {start:"15:30",id:16},
        {start:"16:00",id:17},
        {start:"16:30",id:18},
        {start:"17:00",id:19},
        {start:"17:30",id:20},
        {start:"18:00",id:21},
      ],
      audiences:[
        {name:"Аудитория 1",
        freeTime:[
        {},
        {start:"8:00",id:1},
        {start:"8:30",id:2},
        {start:"9:00",id:3},
        {start:"9:30",id:4},
        {start:"10:00",id:5},
        {start:"10:30",id:6},
        {start:"11:00",id:7},
        {start:"11:30",id:8},
        {start:"12:00",id:9},
        {start:"12:30",id:10},
        {start:"13:00",id:11},
        {start:"13:30",id:12},
        {start:"14:00",id:13},
        {start:"14:30",id:14},
        {start:"15:00",id:15},
        {start:"15:30",id:16},
        {start:"16:00",id:17},
        {start:"16:30",id:18},
        {start:"17:00",id:19},
        {start:"17:30",id:20},
        {start:"18:00",id:21}]
        },
        {name:"Аудитория 2"},
        {name:"Аудитория 3"},
        {name:"Аудитория 4"},
      ]
    }
  },
  methods:{
      chooseTime(){
          console.log(this.before)
      },
      endLesson(){
        
           return this.time.slice((this.from.id + 1))
          
        },
        // chooseTime() {
        //   this.audiences.forEach(audience =>{
        //     if(audience.freeTime.id){}
        //   })
        // }
    
      }
  }
  

</script>


<style scoped>
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
  padding: 10px 15px;
  position: relative;
  transition: all 0.5s ease;
  text-align: center;
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
