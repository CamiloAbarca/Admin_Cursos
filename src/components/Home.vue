<template>
    <div>
        <b-card v-for="curso in cursos" :key="curso.id" tag="article"
            style="max-width: 20rem; padding: 1%;" class="mb-2">
            <template>
                <img :src="curso.img" alt="Imagen del curso" class="curso-img" />
            </template>
            <b-card-text>
                <h3>{{ curso.nombre }}</h3>
                <br>
                <ul>
                    <li><strong>Costo:</strong> {{ curso.costo }}</li>
                    <li><strong>Duración:</strong> {{ curso.duracion }}</li>
                    <li><strong>Cupos:</strong> {{ curso.cupos }}</li>
                    <li><strong>Completado:</strong> {{ curso.completado ? 'Si' : 'No' }}</li>
                    <li><strong>Fecha de registro:</strong> {{ curso.fecha_registro }}</li>
                    <li><strong>Descripción:</strong> {{ curso.descripcion }}</li>
                </ul>
            </b-card-text>
        </b-card>
    </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
    name: 'Home-component',
    computed: {
        ...mapState(['cursos'])
    }
}
</script>

<style scoped>
div {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding: 20px;
    gap: 20px;
}

.b-card {
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.b-card-text {
    font-family: Arial, sans-serif;
    font-size: 14px;
    line-height: 1.5;
}

ul {
    list-style-type: none;
    padding: 0;
    text-align: start;
}

li {
    margin-bottom: 5px;
}

.curso-img {
    width: 150px;
    height: 150px;
    object-fit: contain;
    border-radius: 8px;
    display: block;
    margin: 0 auto;
}

.b-card-title {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
}
</style>