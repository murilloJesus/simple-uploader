<script setup>  
  import { reactive } from 'vue';
  import axios from 'axios'


  const files = reactive([])

  function send(event) {
    let file = event.target.files[0]

    const formData = new FormData()
    formData.append("file", file)

    axios.post('http://127.0.0.1:8000/api/upload', formData)
    .then(response => {
      files.push(response.data.path)
    })
    .catch(error => {
      alert("Erro")
      console.log(error)
    })
  }

</script>

<template>
  <div class="container">
    <div class="d-flex justify-content-center mt-5 w-100">
      <div class="border border-secondary rounded p-3 w-50">
        <label class="form-label" for="file-uploader">Adicionar arquivos</label>
        <input type="file" @change="send" class="form-control" id="file-uploader" />
      </div>
    </div>
    <div class="d-flex justify-content-center mt-3 w-100">
      <div class="border border-secondary rounded p-3 w-50">
        <h4>Arquivos</h4>
        <hr>
          <ul>
            <li v-for="(file, index) in files" :key="index">
              <a :href="file">{{ file }}</a>
            </li>
          </ul>
      </div>
    </div>
  </div>
</template>