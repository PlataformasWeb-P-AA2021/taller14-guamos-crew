<template>
    <div class="pt-5">
        <form @submit.prevent="update" method="post">
            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="edificio.nombre"
                    v-validate="'required'"
                    name="nombre"
                    placeholder="Ingrese nombre"
                    :class="{'is-invalid': errors.has('edificio.nombre') && submitted}">
                <div class="invalid-feedback">
                    Error en el ingreso de nombre
                </div>
            </div>
            <div class="form-group">
                <label for="direccion">Dirección</label>
                <textarea
                    name="direccion"
                    class="form-control"
                    id="direccion"
                    v-validate="'required'"
                    v-model="edificio.direccion"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('edificio.direccion') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Error en el ingreso de dirección
                </div>
            </div>
            <div class="form-group">
                <label for="ciudad">Ciudad</label>
                <textarea
                    name="direccion"
                    class="form-control"
                    id="direccion"
                    v-validate="'required'"
                    v-model="edificio.ciudad"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('edificio.ciudad') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Error en el ingreso de ciudad
                </div>
            </div>
            <div class="form-group">
                <label for="tipo">tipo</label>
                <textarea
                    name="direccion"
                    class="form-control"
                    id="tipo"
                    v-validate="'required'"
                    v-model="edificio.tipo"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('edificio.tipo') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Error en el ingreso de tipo
                </div>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
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
                url: '',
            },
            submitted: false
        }
    },
    mounted() {
        axios.get('http://127.0.0.1:8000/api/edificios/' + this.$route.params.id + '/')
            .then( response => {
                console.log(response.data)
                this.edificio = response.data
            });
    },
    methods: {
        update: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                axios.put(`http://127.0.0.1:8000/api/edificios/${this.edificio.id}/`,
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
