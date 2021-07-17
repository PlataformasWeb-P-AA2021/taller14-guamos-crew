<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <h2><router-link to="/index">Administración de Edificios</router-link></h2>
        <router-link to="/create" class="btn btn-sm btn-primary">+ Edificios</router-link>
        <br>
        <router-link to="/departamentoslist" class="btn btn-sm btn-primary">ver Departamentos</router-link>
        <br>
        <router-link to="" class="btn btn-sm btn-primary">+ Departamentos</router-link>

        <router-view />
      </div>
    </div>
  </div>
</template>