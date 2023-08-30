<template>
    <div>
        <h2>Aplicación de Composition API (con 'setup' en la etiqueta script) - Vue 3</h2>
        <input type="text" placeholder="Mensaje" v-model="message">
        <h3>Cantidad de caracteres {{ numberOfChars }} </h3>

        <div class="file-box">
            <label for="fileInput" class="file-label">Seleccionar Archivo</label>
            <input id="fileInput" type="file" @change="handleFileChange">
        </div>

        <button @click="clearFileContent">Borrar Contenido de Archivo</button>

        <div class="file-content-box" v-if="fileList.length > 0">
            <div v-for="(file, index) in fileList" :key="index" class="file-entry">
                <h4>Nombre del Archivo:</h4>
                <div>{{ file.name }}</div>

                <h4>Contenido del Archivo:</h4>
                <pre>{{ file.content }}</pre>

                <button @click="removeFile(index)">Eliminar Archivo</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
let message = ref('')
const numberOfChars = computed(() => message.value.length)

const fileList = ref([])

const handleFileChange = event => {
    const file = event.target.files[0]
    if (file) {
        const reader = new FileReader()
        reader.onload = event => {
            const fileData = {
                name: file.name,
                content: event.target.result
            }
            fileList.value.push(fileData)
        }
        reader.readAsText(file)
    }
}

const removeFile = index => {
    fileList.value.splice(index, 1)
}

const clearFileContent = () => {
    fileList.value = []
}
</script>

<style scoped>
.file-box {
    border: 1px solid #ccc;
    padding: 10px;
    display: inline-block;
    margin-bottom: 10px;
}

.file-label {
    display: block;
    margin-bottom: 5px;
}

.file-content-box {
    border: 1px solid #ccc;
    padding: 10px;
    margin-top: 10px;
}

.file-entry {
    border: 1px solid #ccc;
    padding: 10px;
    margin-top: 10px;
}

button {
    margin-top: 10px;
}
</style>
