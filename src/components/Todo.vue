<template>
  <div>
       
          <div class="container">
             <h2 class="text-center mt-5">Todo App </h2>

            <div class="d-flex">
             <input v-model='task' type="Text" placeholder="Enter task" class="form-control">
             <button @click="submitform" class="btn btn-warning rounded-0">Submit</button>
            </div>

              <table class="table table-bordered mt-5">

                    <thead>

                            <tr>
                                <th scope="col">Task</th>
                                <th scope="col">Satus</th>
                                <th scope="col" class="text-center">#</th>
                                <th scope="col" class="text-center">#</th>
                             </tr>

                    </thead>

                    <tbody>

                             <tr v-for="(task,index) in tasks" :key="index">
                                <td>{{task.name}}</td>
                                <td  style="width:120px" class="pointer" @click="statuschange(index)">{{task.status}}</td>
                                <td>
                                    <div class="text-center pointer "  @click="Updatetask(index)">
                                        <span class="fa fa-pen"></span>
                                    </div>
                                </td>
                                <td>
                                     <div class="text-center pointer " @click="Deletetask(index)">
                                          <span class="fa fa-trash"></span>
                                       </div>
                                 </td>
                              </tr>


                    </tbody>
               </table>  

          </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data()
  {
        return{
              task:'',
              editedtext:null,
              availablestatus :[ 'to-do' , 'in-Progress', 'finsih'],
              tasks:[
                  {
                      name:'Go to grocery',
                      status:'to-do'
                  },

                   {
                      name:'Go to medical shop',
                      status:'to-do'
                  }

              ]
        }
  },

  methods:{
          
          
          submitform()
          {
                 if(this.task.length === 0) return;

              if(this.editedtext === null)
              {
                 this.tasks.push({
                      name:this.task,
                      status:'to-do'
                 })

                 this.task="";
              }
              else
              {
                   this.tasks[this.editedtext].name = this.task;
                   this.task="";
                   this.editedtext=null;
              }
          },

          Deletetask(index)
          {
                this.tasks.splice(index,1);
          },

          Updatetask(index)
          {
                 this.task = this.tasks[index].name;
                 this.editedtext = index;

          },

          statuschange(index)
          {
                  let newindex = this.availablestatus.indexOf(this.tasks[index].status);
                  newindex++;
                  if(newindex>2)
                   newindex = 0 ;
                  
                  this.tasks[index].status= this.availablestatus[newindex];
          }

  }

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.pointer {
    cursor: pointer;
}
</style>
