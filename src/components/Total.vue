<template>
    <div class="container">
        <div class="alumnos-permitidos">
            <b-icon icon="people-fill"></b-icon>
            Cantidad total de alumnos permitidos: <strong>{{ totalCupos }}</strong> alumnos.
        </div>
        <div class="alumnos-inscritos">
            <b-icon icon="person-check-fill"></b-icon>
            Cantidad total de alumnos inscritos: <strong>{{ totalInscritos }}</strong> alumnos.
        </div>
        <div class="cupos-restantes">
            <b-icon icon="person-plus-fill"></b-icon>
            Cantidad total de cupos restantes: <strong>{{ totalCupos - totalInscritos }}</strong> alumnos.
        </div>
        <div class="cursos-terminados">
            <b-icon icon="clipboard-x"></b-icon>
            Cantidad total de cursos terminados: <strong>{{ totalCursosTerminados }}</strong> cursos.
        </div>
        <div class="cursos-activos">
            <b-icon icon="clipboard-check"></b-icon>
            Cantidad total de cursos activos: <strong>{{ totalCursos - totalCursosTerminados }}</strong> cursos.
        </div>
        <div class="total-cursos">
            <b-icon icon="clipboard"></b-icon>
            Cantidad total de cursos: <strong>{{ totalCursos }}</strong> cursos.
        </div>
    </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
    name: 'Total-component',
    computed: {
        ...mapGetters([
            'totalCursosTerminados',
            'totalCursos',
            'totalCupos',
            'totalInscritos'
        ])
    }

}
</script>

<style>
.alumnos-permitidos {
    border: 2px solid #8615a4;
    color: #8615a4;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}

.alumnos-inscritos {
    border: 2px solid #2899f4;
    color: #2899f4;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}

.cupos-restantes {
    border: 2px solid #e4332f;
    color: #e4332f;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}

.cursos-terminados {
    border: 2px solid #d81d61;
    color: #d81d61;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}

.cursos-activos {
    border: 2px solid #776b02;
    color: #776b02;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}

.total-cursos {
    border: 2px solid #f46f00;
    color: #f46f00;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 2%;
    text-align: start;
}
</style>