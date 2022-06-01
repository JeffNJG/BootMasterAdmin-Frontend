<template>
  <div class="flex justify-center md:my-8">
    <div class="block p-6 rounded-lg shadow-lg bg-white max-w-sm">
      <form method="post" enctype="multipart/form-data">
        <div class="form-group mb-6">
          <label for="title" class="form-label inline-block mb-2 text-gray-700">Title</label>
          <input type="text"
            class="form-control
                    block
                    w-full
                    px-3
                    py-1.5
                    text-base
                    font-normal
                    text-gray-700
                    bg-white bg-clip-padding
                    border border-solid border-gray-300
                    rounded
                    transition
                    ease-in-out
                    m-0
                    focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" 
            id = "title"
            aria-describedby = "titleHelp"
            v-model = "form.title">
          <small id="titleHelp"
            class="block mt-1 text-xs text-gray-600">Ex : Ubuntu 20.04 LTS</small>
        </div>
        <div class="form-group mb-6">
          <label for="model" class="form-label inline-block mb-2 text-gray-700">Model</label>
          <select
            class="form-select appearance-none
                    block
                    w-full
                    px-3
                    py-1.5
                    text-base
                    font-normal
                    text-gray-700
                    bg-white bg-clip-padding bg-no-repeat
                    border border-solid border-gray-300
                    rounded
                    transition
                    ease-in-out
                    m-0
                    focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
            aria-label="Model select"
            id = "model"
            v-model="form.model">
            <option value="Linux">Linux</option>
            <option value="Windows">Windows</option>
            <option value="Macintosh">Macintosh</option>
          </select>
        </div>
        <div class="form-group mb-6">
          <label for="distribution" class="form-label inline-block mb-2 text-gray-700">Distribution</label>
          <select
            class="form-select appearance-none
                    block
                    w-full
                    px-3
                    py-1.5
                    text-base
                    font-normal
                    text-gray-700
                    bg-white bg-clip-padding bg-no-repeat
                    border border-solid border-gray-300
                    rounded
                    transition
                    ease-in-out
                    m-0
                    focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
            aria-label="Model select"
            id = "distribution"
            v-model="form.distribution">
            <option value="Ubuntu">Ubuntu</option>
            <option value="Debian">Debian</option>
            <option value="Fedora">Fedora</option>
          </select>
        </div>
        <div class="mb-3">
          <label for="domain" class="form-label inline-block mb-2 text-gray-700">Domain</label>
          <select
            class="form-select appearance-none
                    block
                    w-full
                    px-3
                    py-1.5
                    text-base
                    font-normal
                    text-gray-700
                    bg-white bg-clip-padding bg-no-repeat
                    border border-solid border-gray-300
                    rounded
                    transition
                    ease-in-out
                    m-0
                    focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
            aria-label="Domain select"
            id = "domain"
            v-model="form.domain">
            <option value="Client">Client</option>
            <option value="Server">Server</option>
        </select>
      </div>
        <div class="form-group mb-6">
          <label for="description" class="form-label inline-block mb-2 text-gray-700">Description</label>
          <textarea
            class="form-control
                  block
                  w-full
                  px-3
                  py-1.5
                  text-base
                  font-normal
                  text-gray-700
                  bg-white bg-clip-padding
                  border border-solid border-gray-300
                  rounded
                  transition
                  ease-in-out
                  m-0
                  focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
            id="description"
            rows="3"
            aria-describedby="descriptionHelp"
            v-model="form.description"></textarea>
            <small id="descriptionHelp"
            class="block mt-1 text-xs text-gray-600">Some statements about the os you upload.</small>
        </div>
        <div class="mb-3">
          <label for="ressource"
            class="form-label inline-block mb-2 text-gray-700">Choose the file</label>
          <input class="form-control
                      block
                      w-full
                      px-3
                      py-1.5
                      text-base
                      font-normal
                      text-gray-700
                      bg-white bg-clip-padding
                      border border-solid border-gray-300
                      rounded
                      transition
                      ease-in-out
                      m-0
                      focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
                  type="file"
                  @change="onFileChange">
        </div>
        <button type="submit" class="
          px-6
          py-2.5
          bg-blue-600
          text-white
          font-medium
          text-xs
          leading-tight
          uppercase
          rounded
          shadow-md
          hover:bg-blue-700 hover:shadow-lg
          focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0
          active:bg-blue-800 active:shadow-lg
          transition
          duration-150
          ease-in-out"
          @click="submitData">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default ({
    name: "AddSystem",
    data () {
      return {
        form : {
          title: '',
          model: '',
          distribution: '',
          domain: '',
          description: ''
        },
        file : ''
      }
    },
    methods : {
      onFileChange(e) {
        const ress = e.target.files[0]; // accessing file
        this.file = ress;
      },
      submitData() {
        let formData = new FormData();
        for (var key in this.form) {
          formData.append(key, this.form[key]);
        }
        formData.append('file', this.file);
        axios.post('http://localhost:3000/api/stuff', formData).then(
          (res) => {
            if (res.status === 200) {
              this.$router.push({ path : '/' });
            }
          }
        ).catch(
          (error) => {
            console.log(error);
          }
        )
      }
    }
  })
</script>
