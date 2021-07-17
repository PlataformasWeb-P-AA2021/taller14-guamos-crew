<template>
    <div class="pt-5">
        <form @submit.prevent="create" method="post">
            <div class="form-group">
                <label for="nombre">nombre</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="departamento.nombre"
                    v-validate="'required'"
                    name="nombre"
                    placeholder="Ingrese nombre"
                    :class="{'is-invalid': errors.has('departamento.nombre') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid name.
                </div>
            </div>

            <div class="form-group">
                <label for="costo_dept">Costo del departamento</label>
                <input
                    type="text"
                    class="form-control"
                    id="costo_dept"
                    v-model="departamento.costo_dept"
                    v-validate="'required'"
                    name="costo_dept"
                    placeholder="Ingrese el costo del departamento"
                    :class="{'is-invalid': errors.has('departamento.costo_dept') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid apellido.
                </div>
            </div>

            <div class="form-group">
                  <label for="num_dept">Numero del departamento</label>
                  <input
                      type="text"
                      class="form-control"
                      id="num_dept"
                      v-model="departamento.num_dept"
                      v-validate="'required'"
                      name="num_dept"
                      placeholder="Ingrese el numero del departamento"
                      :class="{'is-invalid': errors.has('departamento.num_dept') && submitted}">
                  <div class="invalid-feedback">
                      Please provide a valid apellido.
                  </div>
              </div>

              <div class="form-group">
                  <label for="num_cuarto">Numero de cuartos</label>
                  <input
                      type="text"
                      class="form-control"
                      id="num_cuarto"
                      v-model="departamento.num_cuarto"
                      v-validate="'required'"
                      name="num_cuarto"
                      placeholder="Ingrese el numero de cuartos"
                      :class="{'is-invalid': errors.has('departamento.num_cuarto') && submitted}">
                  <div class="invalid-feedback">
                      Please provide a valid apellido.
                  </div>
              </div>

            <div class="form-group">
                <label for="edificio">edificio</label>
                <select id="edificio" v-model="departamento.edificio">
                            <option v-for="e in edificiosList" :key="e.url" :value="e.url">{{ e.nombre }}</option>
                        </select>
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
            departamento: {
                nombre: '',
                costo_dept: '',
                num_dept: '',
                num_cuarto: '',
                edificio: '',
            },
            edificiosList: [],
            submitted: false
        }
    },
    mounted() {
        this.getedificiosList(),
        axios.get('http://127.0.0.1:8000/api/departamentos/' + this.$route.params.id + '/')
            .then( response => {
                console.log(response.data)
                this.departamento = response.data
        });
    },
    methods: {
      getedificiosList() {
            axios
            .get('http://127.0.0.1:8000/api/edificios/')
            .then(response => {
                this.edificiosList = response.data
            })
            .catch(error => {
                console.log(error)
            })

        },
        create: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                axios.put(`http://127.0.0.1:8000/api/departamentos/${this.departamento.id}/`,
                        this.departamento
                    )
                    .then(response => {
                        this.$router.push('/departamentoslist');
                    })
            });
        }
    },
}
</script>
