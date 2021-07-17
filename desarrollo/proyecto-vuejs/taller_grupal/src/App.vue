<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <h2><router-link to="/index">Administración de Edificios</router-link></h2>
        <router-link to="/create" class="btn btn-sm btn-primary">+ Edificios</router-link>
        <br>
<<<<<<< HEAD
        <router-link to="/listdept" class="btn btn-sm btn-primary">ver Departamentos</router-link>
=======
        <router-link to="/departamentoslist" class="btn btn-sm btn-primary">ver Departamentos</router-link>
>>>>>>> 525fab9f500ce8974e1d8c3cbd305a1dc782346f
        <br>
        <router-link to="/createdept" class="btn btn-sm btn-primary">+ Departamentos</router-link>

        <router-view />
      </div>
    </div>
  </div>
</template>