<template>
    <div>
        <h2>Aplicación de Composition API (con 'setup' en la etiqueta script) - Vue 3</h2>
        <input type="text" placeholder="Mensaje" v-model="message">
        <h3>Cantidad de caracteres {{ numberOfChars }} </h3>

        <input type="file" @change="handleFileChange">
        <button @click="clearFileContent">Borrar Contenido de Archivo</button>

        <div>
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

const handleFileChange = event => {
    const file = event.target.files[0]
    if (file) {
        const reader = new FileReader()
        reader.onload = event => {
            fileContent.value = event.target.result
        }
        reader.readAsText(file)
    }
}

const clearFileContent = () => {
    fileContent.value = ''
}
</script>

<style scoped></style>
