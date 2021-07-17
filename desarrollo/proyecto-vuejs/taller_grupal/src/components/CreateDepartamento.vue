<template>
    <div className="pt-5">
        <form @submit.prevent="create" method="post">
            <div className="form-group">
                <label htmlFor="nombre">Propietario</label>
                <input
                type="text"
                className="form-control"
                id="nombre"
                v-model="departamento.nombre"
                v-validate="'required'"
                name="departamento"
                placeholder="Ingresar propietario"
                :class="{'is-invalid': errors.has('departamento.nombre') && submitted}">
                <div className="invalid-feedback">
                    Please provide a valid name.
                </div>
            </div>

            <div className="form-group">
                <label htmlFor="costo_dept">Costo del departamento</label>
                <input
                type="text"
                className="form-control"
                id="costo_dept"
                v-model="departamento.costo_dept"
                v-validate="'required'"
                name="costo_dept"
                placeholder="Ingrese costo de departamento"
                :class="{'is-invalid': errors.has('departamento.costo_dept') && submitted}">
                <div className="invalid-feedback">
                    Please provide a valid apellido.
                </div>
            </div>

            <div className="form-group">
                <label htmlFor="num_dept">Numero de departamento</label>
                <input
                    type="text"
                    className="form-control"
                    id="num_dept"
                    v-model="departamento.num_dept"
                    v-validate="'required'"
                    name="num_dept"
                    placeholder="Ingrese el numero del departamento"
                    :class="{'is-invalid': errors.has('departamento.num_dept') && submitted}">
                <div className="invalid-feedback">
                    Please provide a valid apellido.
                </div>
            </div>

            <div className="form-group">
                <label htmlFor="num_cuarto">Numero de cuartos</label>
                <input
                    type="text"
                    className="form-control"
                    id="num_cuarto"
                    v-model="departamento.num_cuarto"
                    v-validate="'required'"
                    name="num_cuarto"
                    placeholder="Ingrese numero de cuartos"
                    :class="{'is-invalid': errors.has('departamento.num_cuarto') && submitted}">
                <div className="invalid-feedback">
                    Please provide a valid apellido.
                </div>
            </div>

        <div className="form-group">
            <br>
            <label htmlFor="edificio">edificio</label>
            <select v-model="departamento.edificio">
                <option v-for="e in edificiosList" :key="e.url" :value="e.url">{{ e.nombre }}</option>
            </select>
        </div>
        <br>
        <button type="submit" className="btn btn-primary">Crear</button>
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
        num_cuarto:'',
        edificio:'',
      },
      edificiosList: [],
      submitted: false
    }
  },
  mounted() {
    this.getEdificioList()
  },
  methods: {
    getEdificioList() {
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
        axios.post('http://127.0.0.1:8000/api/departamentos/',
            this.departamento
        )
            .then(response => {
              this.$router.push('/departamentos');
            })
      });
    }
  },
}
</script>
