<template>
    <div>
        <h2>Aplicación de Composition API (con 'setup' en la etiqueta script) - Vue 3</h2>
        <input type="text" placeholder="Mensaje" v-model="message">
        <h3>Cantidad de caracteres {{ numberOfChars }} </h3>

        <div class="file-box">
            <label for="fileInput" class="file-label">Seleccionar Archivo</label>
            <input id="fileInput" type="file" @change="handleFileChange">
            <div class="file-name">{{ fileName }}</div>
        </div>

        <button @click="clearFileContent">Borrar Contenido de Archivo</button>

        <div class="file-content-box">
            <div v-if="fileName" class="file-name-above">
                <h4>Nombre del Archivo:</h4>
                <div>{{ fileName }}</div>
            </div>

            <h4>Contenido del Archivo:</h4>
            <pre>{{ fileContent }}</pre>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
let message = ref('')
const numberOfChars = computed(() => message.value.length)

const fileContent = ref('')
const fileName = ref('')

const handleFileChange = event => {
    const file = event.target.files[0]
    if (file) {
        fileName.value = file.name;
        const reader = new FileReader()
        reader.onload = event => {
            fileContent.value = event.target.result
        }
        reader.readAsText(file)
    }
}

const clearFileContent = () => {
    fileContent.value = ''
    fileName.value = ''
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

.file-name {
    font-weight: bold;
    margin-bottom: 5px;
}

.file-content-box {
    border: 1px solid #ccc;
    padding: 10px;
    margin-top: 10px;
}

.file-name-above {
    margin-bottom: 10px;
    padding-bottom: 10px;
    border-bottom: 1px solid #ccc;
    text-align: center;
}
</style>
