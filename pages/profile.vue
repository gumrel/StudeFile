<script setup>
  import { ref, onMounted } from 'vue'
  import httpService from '~/services/httpService';

  import profileInfo from './profileInfo.vue';


  const user = ref(null)

  const fetchMe = async () => {
    try{const {data} = await httpService.get('private/users/me')
    user.value = data.value
    
  }
      catch{
        console.error('errorAH', error);
      }
  }
  onMounted(fetchMe)


</script>

<template>

<div class="layout-main">
    <div class="p-card p-component overflow-hidden shadow">

      <div class="p-card-body ">

        <div class="p-card-caption ">
          <div class="p-card-title"><p class="font-bold text-xl text-indigo-500	pb-3">User Information</p></div>
        </div>

        <div class="p-card-content">
          
          <profileInfo
            v-if="user"
            :nickname="user.nickname"
            :email="user.email"
            :created_at="user.created_at"
            :description="user.description"
          />

          </div>
          {{ user }}
        </div>
      </div>
    
        

    </div>
</template>

<style scoped></style>


