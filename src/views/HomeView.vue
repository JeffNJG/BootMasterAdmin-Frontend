<template>
  <div class="home">
    <div class="flex flex-col container">
      <div class="overflow-x-auto sm:-mx-6 md:-mx-3">
        <div class="py-4 inline-block min-w-full sm:px-6 lg:px-8">
          <div class="overflow-hidden">
            <table class="text-center min-w-full">
              <thead class="border-b bg-gray-800">
                <tr>
                  <th scope="col" class="text-sm font-medium text-white px-6 py-4">
                    #
                  </th>
                  <th scope="col" class="text-sm font-medium text-white px-6 py-4">
                    Title
                  </th>
                  <th scope="col" class="text-sm font-medium text-white px-6 py-4">
                    Domain
                  </th>
                  <th scope="col" class="text-sm font-medium text-white px-6 py-4">
                    Ressource
                  </th>
                  <th scope="col" class="text-sm font-medium text-white px-6 py-4">
                    X
                  </th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(system, index) in systems" :key="system._id" class="bg-white border-b">
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{{ index+1 }}</td>
                  <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                    {{ system.title }}
                  </td>
                  <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                    {{ system.domain }}
                  </td>
                  <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap">
                    {{ system.ressource }}
                  </td>
                  <td class="text-sm text-orange-500 px-6 py-4 whitespace-nowrap">
                    <span class="hover:cursor-pointer hover:underline" @click="deleteSystem(system._id)">Modifier</span>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'HomeView',
    data() {
      return {
        systems : []
      }
    },
    created() {
      axios.get('http://localhost:3000/api/stuff').then(
        (res) => {
          console.log('Status : ' + res.statusText)
          this.systems = res.data;
          console.log(this.systems);
        }
      ).catch(
        (error) => {
          console.log(error);
        }
      );
    },
    methods : {
      deleteSystem(id) {
        const url = 'http://localhost:3000/api/stuff/' + id;
        axios.delete(url).then(
          (res) => {
            if (res.status === 200) {
              this.$router.push({ path : '/' });
            }
          }
        ).catch(
          (err) => {
            alert(err);
          }
        );
      }
    }
  }
</script>
