<template class="container">
    <h1>Cargue Excel</h1>

    <div class="cargueArchivo">
        <input type="file" class="form-control " id="inputGroupFile01" @change="cambioDeArchivo">
    </div>
    <div class="container px-4 text-center">
        <div class="row gx-5">
            <div class="col">
                <div class="p-3 border bg-light shadow p-3 mb-5 bg-body rounded">
                    <dl>
                        <h4 class="fw-bold">Documento o Nit</h4>
                        <dt v-for="(item, i ) in items" :key="i">{{ item }}</dt>
                    </dl>
                </div>
            </div>
            <div class="col">
                <!--componente hijo-->
                <div class="ventan p-3 border bg-light shadow p-3 mb-5 bg-body rounded" >
                    <h3 class="fw-bold">Codigo a insertar </h3>
                    <ExportHtml :items="items" />
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { ref } from 'vue';
import readXlsFile from 'read-excel-file'; //biblioteca me permite trabajar con archivos xls
import ExportHtml from './ExportHtml.vue'

const items = ref(); // Guardamos los datos procesados por readXlsFile

const cambioDeArchivo = async (e) => {
    const file = e.target.files[0]; // Obtiene el archivo seleccionado por el evento change
    if (!file) return; // Verifica si se seleccionó un archivo y sale de la función si no hay ninguno.

    try {
        const rows = await readXlsFile(file);
        items.value = rows ? rows.flat() : []; // Asegúrate de que rows no sea undefined antes de intentar aplanar

    } catch (error) {
        console.error("Error al procesar el archivo Excel:", error);
    }
}
</script>
  
<style>
.cargueArchivo {
    margin-right: 35%;
    margin-left: 35%;
    margin-bottom: 2%;
   
}

</style>                                
