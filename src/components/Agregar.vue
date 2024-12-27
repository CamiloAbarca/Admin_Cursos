<template>
    <div class="container">
        <b-button v-b-modal.modal-form style="background-color: #1976d2; border: #5599db">AGREGAR CURSO</b-button>

        <b-modal id="modal-form" title="Formulario de Registro" hide-footer hide-header>
            <b-form @submit.prevent="submitForm">
                <b-form-group label="Nombre" label-for="input-nombre">
                    <b-form-input id="input-nombre" v-model="form.nombre" required></b-form-input>
                </b-form-group>

                <b-form-group label="URL de la imagen" label-for="input-url">
                    <b-form-input id="input-url" type="url" v-model="form.img" required></b-form-input>
                </b-form-group>

                <b-form-group label="Cupos del curso" label-for="input-cupos">
                    <b-form-input id="input-cupos" type="number" v-model="form.cupos" required></b-form-input>
                </b-form-group>

                <b-form-group label="Inscritos en el curso" label-for="input-inscritos">
                    <b-form-input id="input-inscritos" type="number" v-model="form.inscritos" required></b-form-input>
                </b-form-group>

                <b-form-group label="Duración del curso" label-for="input-duracion">
                    <b-form-input id="input-duracion" type="number" v-model="form.duracion" required></b-form-input>
                </b-form-group>

                <b-form-group label="Fecha de registro" label-for="input-fecha">
                    <b-form-input id="input-fecha" type="date" v-model="form.fecha_registro" disabled></b-form-input>
                </b-form-group>

                <b-form-group label="Costo del curso" label-for="input-costo">
                    <b-form-input id="input-costo" type="number" v-model="form.costo" required></b-form-input>
                </b-form-group>
                <br>

                <b-form-textarea id="descripcion" v-model="form.descripcion" placeholder="Descripción del curso"
                    rows="3" max-rows="6"></b-form-textarea>
                <br>

                <div class="button-group">
                    <b-button type="submit" variant="success">AGREGAR</b-button>
                    <b-button variant="warning" @click="limpiarForm">LIMPIAR FORMULARIO</b-button>
                    <b-button variant="danger" @click="$bvModal.hide('modal-form')">CANCELAR</b-button>
                </div>

                <b-alert v-if="errorMessage" variant="danger" dismissible @dismissed="errorMessage = ''">
                    {{ errorMessage }}
                </b-alert>
            </b-form>
        </b-modal>
    </div>
</template>

<script>
import { mapMutations } from 'vuex';

export default {
    name: 'Agregar-component',
    data() {
        return {
            form: {
                img: '',
                nombre: '',
                costo: null,
                duracion: null,
                cupos: null,
                inscritos: null,
                completado: false,
                fecha_registro: this.getCurrentDate(),
                descripcion: ''
            },
            errorMessage: ''
        };
    },

    methods: {
        ...mapMutations(['agregarCurso']),

        getCurrentDate() {
            const today = new Date();
            const year = today.getFullYear();
            const month = String(today.getMonth() + 1).padStart(2, '0');
            const day = String(today.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        },

        limpiarForm() {
            this.form = {
                img: '',
                nombre: '',
                costo: '',
                duracion: '',
                cupos: '',
                inscritos: '',
                completado: false,
                fecha_registro: this.getCurrentDate(),
                descripcion: ''
            };
        },

        submitForm() {
            if (this.form.inscritos > this.form.cupos) {
               alert('El número de inscritos no puede ser mayor que el número de cupos.');
                return;
            }

            const fechaParts = this.form.fecha_registro.split('-');
            const fechaFormateada = `${fechaParts[2]}/${fechaParts[1]}/${fechaParts[0]}`;

            const curso = {
                ...this.form,
                fecha_registro: fechaFormateada,
                costo: Number(this.form.costo),
                duracion: `${this.form.duracion} ${this.form.duracion > 1 ? 'meses' : 'mes'}`,
                cupos: Number(this.form.cupos),
                inscritos: Number(this.form.inscritos),
            };

            this.agregarCurso(curso);
            this.limpiarForm();
            this.$bvModal.hide('modal-form');
        }
    }
}
</script>

<style scoped>
.container {
    margin-top: 20px;
}

.button-group {
    display: flex;
    gap: 10px;
}
</style>