<template>
    <div class="pt-5">
        <form @submit.prevent="create" method="post">
            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="edificio.nombre"
                    v-validate="'required'"
                    name="nombre"
                    placeholder="Ingres su nombre"
                    :class="{'is-invalid': errors.has('edificio.nombre') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid name.
                </div>
            </div>

            <div class="form-group">
                <label for="direccion">Dirección</label>
                <input
                    type="text"
                    class="form-control"
                    id="direccion"
                    v-model="edificio.direccion"
                    v-validate="'required'"
                    name="direccion"
                    placeholder="Ingrese su Direccion"
                    :class="{'is-invalid': errors.has('edificio.direccion') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid apellido.
                </div>
            </div>

            <div class="form-group">
                <label for="ciudad">Ciudad</label>
                <input
                    type="text"
                    class="form-control"
                    id="ciudad"
                    v-model="edificio.ciudad"
                    v-validate="'required'"
                    name="apellido"
                    placeholder="Ingrese la ciudad"
                    :class="{'is-invalid': errors.has('edificio.ciudad') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid cedula.
                </div>
            </div>

            <div class="form-group">
                <label for="tipo">Tipo</label>
                <input
                    type="text"
                    class="form-control"
                    id="tipo"
                    v-model="edificio.tipo"
                    v-validate="'required'"
                    name="apellido"
                    placeholder="Ingrese el tipo"
                    :class="{'is-invalid': errors.has('edificio.tipo') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid correo.
                </div>
            </div>
            <button type="submit" class="btn btn-primary">Crear</button>
        </form>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    data() {
        return {
            edificio: {
                nombre: '',
                direccion: '',
                ciudad: '',
                tipo: '',
            },
            submitted: false
        }
    },
    methods: {
        create: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                console.log(this.correo)
                axios.post('http://127.0.0.1:8000/api/edificios/',
                        this.edificio
                    )
                    .then(response => {
                        this.$router.push('/');
                    })
            });
        }
    },
}
</script>
