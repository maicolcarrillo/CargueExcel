<template>
    <div>
        <ol>
            <li v-for="(element, index) in props.items" :key="index">
                {{ codeHtml(element) }}
            </li>

        </ol>
    </div>
</template>
  
<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    items: { type: Array, required: true }
})

const codeHtml = (element) => {
    if (element == element.number) {
        return `<option value="cp08_document|lk|${element}">Identificación como ${element}</option>`;
    }
    return `<option value="cs18_login|eq|${element}">Usuario = ${element}</option>`
}

//const emits = defineEmits(['buttonClick'])

/*const emitEvent = () => {
    emits('buttonClick', 'Hola');
}}*/    

</script>

