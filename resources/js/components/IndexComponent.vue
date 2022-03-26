<template>
    <div>
<table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Age</th>
      <th scope="col">Job</th>
      <th scope="col">Edit</th>
      <th scope="col">Delete</th>
    </tr>
  </thead>
  <tbody>
    <template v-for="person in people">
    <ShowComponent :person="person" :ref="`show_${person.id}`"></ShowComponent>
    <EditComponent :person="person" :ref="`edit_${person.id}`"></EditComponent>
</template>
  </tbody>
</table>
    </div>
</template>

<script>

import EditComponent from "./EditComponent.vue";
import ShowComponent from "./ShowComponent.vue";

export default {
    name: "IndexComponent",

    data(){
        return{
            people: null,
            editPersonId: null,
            name: null,
            age: null,
            job: null
        }
    },


    
    mounted() {
        this.getPeople()

  
    },

    components: {
        EditComponent,
        ShowComponent,
    },

    methods: {
            getPeople(){
                axios.get('/api/people')
                .then(res => {
                    this.people = res.data;
                })
            },

          

          
            isEdit(id){
              return this.editPersonId === id
            },

            indexLog(){
              console.log('this is index component');
            }
        }
    }

</script>

<style scoped>

</style>