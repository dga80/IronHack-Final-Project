<template>
       <section class="flex mx-5 mt-5"> 
          <div class="">
            
            <div class="pb-2">      
              <RouterLink class="flex items-center" to="/dashboard/user"  >
                <svg class="h-7 text-sky-900"  fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z"/>
              </svg>
                <h4 class="text-l pl-2  text-sky-900">User</h4>
              </RouterLink>
            </div>

            <div class="pb-1">           
              <RouterLink class="flex items-center" to="/dashboard/tasks">
                <svg class="h-6 ml-1 text-sky-900"  viewBox="0 0 24 24"  fill="none"  stroke="currentColor"  stroke-width="2"  stroke-linecap="round"  stroke-linejoin="round">  <path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z" />  <line x1="9npm ryun dev
                  " y1="14" x2="15" y2="14" /></svg>
                <h4 class="text-l pl-2  text-sky-900"> Tasks</h4>
              </RouterLink>
            </div>
            
            <div class="">
              <RouterLink class="flex items-center" to="/dashboard/archived">
                <svg class="h-8 ml-1 text-sky-900"  width="24" height="24" viewBox="0 0 24 24"  fill="none"  stroke="currentColor"  stroke-width="2"  stroke-linecap="round"  stroke-linejoin="round">  <path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z" />  <line x1="9" y1="14" x2="15" y2="14" /></svg>
                <h4 class="text-l pl-2 text-sky-900">Archived</h4>
              </RouterLink>  
            </div> 

            <div class="">
              <RouterLink class="flex items-center" to="/dashboard/contact">
                <svg class="h-8 ml-1 text-sky-900"  width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">  <path stroke="none" d="M0 0h24v24H0z"/>  <rect x="4" y="13" rx="2" width="5" height="7" />  <rect x="15" y="13" rx="2" width="5" height="7" />  <path d="M4 15v-3a8 8 0 0 1 16 0v3" /></svg>
                <h4 class="text-l pl-2  text-sky-900">Contact us</h4>
              </RouterLink>  
            </div> 
          </div>
      </section>  

      <section class="">
        <div class="">
        <h1 class=" ml-6 mb-[-20px] mt-10 text-sky-900 opacity-50">≥ ADD NEW TASK</h1>
          <form class=" py-7 mx-5 w-[315px]" @submit.prevent="createNew()">
            <textarea
              type="text"
              placeholder="title"
              v-model="title"
              class=" h-9 w-5/6 border 1 border-grey rounded-lg p-1"/>
              <textarea
              type="text"
              placeholder="description"
              v-model="description"
              class=" h-5/6 w-5/6 border 1 border-grey rounded-lg p-1"/>
            <button
              type="submit"
              class="mt-3 w-5/6 rounded-md text-s text-slate-300 group bg-sky-900 shadow-xl">
              CREATE
            </button>
          </form>   
        </div>
      </section> 

</template>

<script>
    import { RouterLink } from 'vue-router'
    import { mapStores } from "pinia";
    import userStore from "../stores/user";
    import tasksStore from "../stores/tasks";

    export default {
  data() {
    return {
      user_id: null,
      title: null,
      description: null,
      status: "1",
      array: [],
    };
  },

  computed: {
    ...mapStores(userStore, tasksStore),
  },

  methods: {

    async createNew() {
      await this.tasksStore.createTask(
        this.userStore.user.id,
        this.title,
        this.description,
        this.status
      );
      this.title=""
      await this.tasksStore.fetchTasks();
      this.$router.push({ name: "Tasks" }); 
      this.description=""
    },
  },
 };
</script>