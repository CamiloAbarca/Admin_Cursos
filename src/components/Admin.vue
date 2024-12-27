<template>
    <div class="container">
        <br>
        <b-table striped hover :items="cursos" :fields="fields">
            <template #cell(fecha_registro)="data">
                <div class="fecha">{{ data.item.fecha_registro }}</div>
            </template>
            <template #cell(costo)="data">
                <div class="costo">${{ data.item.costo }}</div>
            </template>
            <template #cell(completado)="data">
                <div :class="data.item.completado ? 'terminadoTrue' : 'terminadoFalse'">
                    {{ data.item.completado ? 'Si' : 'No' }}</div>
            </template>
            <template #cell(actions)="data">
                <b-button @click="editCurso(data.item)" style="background-color: transparent; border: none;"><b-icon
                        icon="pencil-fill" style="color: #ffa900;"></b-icon></b-button>
                <b-button @click="confirmDelete(data.item)" style="background-color: transparent; border: none;"><b-icon
                        icon="trash-fill" style="color: #d60202;"></b-icon></b-button>
            </template>
        </b-table>

        <!-- Modal de Confirmación -->
        <b-modal id="confirm-delete-modal" title="Confirmar Eliminación" @ok="deleteCurso" hide-header>
            <p>¿Estás seguro de que deseas eliminar este curso?</p>
        </b-modal>

        <!-- Modal para Editar Curso -->
        <b-modal id="edit-course-modal" title="Editar Curso" @ok="updateCurso" hide-header ok-title="Editar"
            cancel-title="Cerrar" ok-variant="success" cancel-variant="danger">
            <b-form>
                <b-form-group label="Nombre del Curso">
                    <b-form-input v-model="cursoEditado.nombre" required></b-form-input>
                </b-form-group>
                <b-form-group label="Costo">
                    <b-form-input type="number" v-model="cursoEditado.costo" required></b-form-input>
                </b-form-group>
                <b-form-group label="Duración">
                    <b-form-input v-model="cursoEditado.duracion" required></b-form-input>
                </b-form-group>
                <b-form-group label="Cupos">
                    <b-form-input type="number" v-model="cursoEditado.cupos" required></b-form-input>
                </b-form-group>
                <b-form-group label="Inscritos">
                    <b-form-input type="number" v-model="cursoEditado.inscritos" required></b-form-input>
                </b-form-group>
                <br>
                <b-form-group label="Completado">
                    <b-form-checkbox v-model="cursoEditado.completado">¿Curso Completado?</b-form-checkbox>
                </b-form-group>
                <br>
                <b-form-textarea v-model="cursoEditado.descripcion"></b-form-textarea>

                <!-- Mensaje de error -->
                <b-alert v-if="errorMessage" variant="danger">{{ errorMessage }}</b-alert>
            </b-form>
        </b-modal>
    </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex';

export default {
    name: 'AdminComponent',

    data() {
        return {
            cursoAEliminar: null,
            cursoEditado: {},
            errorMessage: ''
        };
    },

    components: {

    },

    computed: {
        ...mapState(['cursos']),
        fields() {
            return [
                { key: 'nombre', label: 'Curso' },
                { key: 'cupos', label: 'Cupos' },
                { key: 'inscritos', label: 'Inscritos' },
                { key: 'duracion', label: 'Duración' },
                { key: 'costo', label: 'Costo' },
                { key: 'completado', label: 'Terminado' },
                { key: 'fecha_registro', label: 'Fecha' },
                { key: 'actions', label: 'Acciones', sortable: false }
            ];
        }
    },

    methods: {
        ...mapMutations(['eliminarCurso']),
        editCurso(curso) {
            this.cursoEditado = { ...curso };
            this.$bvModal.show('edit-course-modal');
        },
        updateCurso() {
            this.cursoEditado.costo = Number(this.cursoEditado.costo);
            this.cursoEditado.cupos = Number(this.cursoEditado.cupos);
            this.cursoEditado.inscritos = Number(this.cursoEditado.inscritos);

            if (this.cursoEditado.inscritos > this.cursoEditado.cupos) {
                alert('El número de inscritos no puede ser mayor que el número de cupos.')
                return
            }

            this.errorMessage = '';
            this.$store.commit('editarCurso', this.cursoEditado);
            this.cursoEditado = {};
            this.$bvModal.hide('edit-course-modal');
        },
        confirmDelete(curso) {
            this.cursoAEliminar = curso;
            this.$bvModal.show('confirm-delete-modal');
        },
        deleteCurso() {
            if (this.cursoAEliminar) {
                this.eliminarCurso(this.cursoAEliminar);
                this.cursoAEliminar = null;
            }
        }
    }
}
</script>


<style scoped>
.fecha,
.costo {
    background-color: #00c853;
    color: white;
    border-radius: 15px;
}

.terminadoTrue {
    background-color: #00b0ff;
    color: white;
    border-radius: 15px;
}

.terminadoFalse {
    background-color: #bcaaa4;
    color: white;
    border-radius: 15px;
}
</style>