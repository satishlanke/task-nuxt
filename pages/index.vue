<template>
<div class="">
  <TableForm
  @submittabledata="dynamicTable"
  />
  <!-- {{info}} -->
  <div class="d-flex justify-content-center mt-5">
    <!-- {{info}} -->
<table>
  <tbody>
    <tr v-for="(a,index) in info" :key="index">
    <td v-for="(b,index) in a" :key="index"><button @click="addData(index)" class="btn btn-info btn-lg mr-3">{{b}}</button></td>
  </tr>
  </tbody>
  </table>
  </div>
  

</div>
</template>

<script>
import Swal from 'sweetalert2'
import axios from 'axios'

import TableForm from "../components/TableForm.vue";
export default {
  name: "IndexPage",
  data() {
    return {
      info: {
        row:'',
        col:''
      },
      row:'',
      col:''
    };
  },
  components: {
    TableForm,
  },
  methods: {
    async dynamicTable(info) {
      this.info.row =info.row;
      this.info.col =info.col
      let params ={
        row:info.row,
        col:info.col
      }
      console.log(params)

      await axios.post('http://localhost:5000/rowcol',params).then((res)=>{
        console.log(res)
        this.info = res.data.result.cols
        this.row = res.data.result.row
        this.col = res.data.result.col

      })
      
      // let table =[]
      // for(let i=0;i<this.info.row;i++){
      //   let obj ={}
      //   for(let j=0;j<this.info.col;j++){
      //     obj[`${i}`+`${j}`]=null
      //   }
      //   table.push(obj)

      // }
      // axios.post('')
      // console.log(table,'table')

      


    },
      addData(id){
         

      // alert(id)
       this.$swal.fire({
          title: "An input!",
          text: "Write something interesting:",
          input: 'text',
          showCancelButton: true        
      }).then((result) => {
          if (result.value) {
              console.log("Result: " + result.value);
              let params ={
                row:this.row,
                col:this.col,
                index:id,
                title:result.value
              }
              console.log(params,'params')
               axios.post('http://localhost:5000/rowcolupdate',params).then((res)=>{
              console.log(res)
              // this.info = res.data.result.cols
              this.info = res.data.result.cols
            })
          }
      });
      
    }
  },
};
</script>


<style scoped>
button{
  /* padding: 1em 3em;  */
    margin: 0.1em 0.5em 0.1em 0.1em;
    width: 100%;
    min-height: 3em;
}
</style>