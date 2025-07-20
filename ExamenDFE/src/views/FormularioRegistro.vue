<template>
  <div class="container mt-5">
    <h2 class="mb-4 text-center">Formulario de Registro</h2>

    <form @submit.prevent="validarFormulario">
      <div class="mb-3">
        <label for="nombre" class="form-label centered-label">Nombre</label>
        <input type="text" v-model="nombre" class="form-control" id="nombre" />
      </div>

      <div class="mb-3">
        <label for="correo" class="form-label centered-label">Correo</label>
        <input type="email" v-model="correo" class="form-control" id="correo" />
        <div v-if="correo && !correoValido" class="text-danger small mt-1">
          Correo inválido.
        </div>
      </div>

      <div class="mb-3">
        <label for="contrasena" class="form-label centered-label">Contraseña</label>
        <input type="password" v-model="contrasena" class="form-control" id="contrasena" />
      </div>

      <div class="mb-3">
        <label for="repetirContrasena" class="form-label centered-label">Repetir Contraseña</label>
        <input type="password" v-model="repetirContrasena" class="form-control" id="repetirContrasena" />
        <div v-if="repetirContrasena && !contrasenasIguales" class="text-danger small mt-1">
          Las contraseñas no coinciden.
        </div>
      </div>

      <div>
        <button type="submit" class="btn btn-purple px-4">
          Enviar
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "FormularioRegistro",
  data() {
    return {
      nombre: "",
      correo: "",
      contrasena: "",
      repetirContrasena: "",
    };
  },
  computed: {
    correoValido() {
      const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return regex.test(this.correo);
    },
    contrasenasIguales() {
      return this.contrasena === this.repetirContrasena;
    },
    formularioCompleto() {
      return (
        this.nombre &&
        this.correoValido &&
        this.contrasena &&
        this.contrasenasIguales
      );
    },
  },
  methods: {
    validarFormulario() {
      if (this.formularioCompleto) {
        alert("✅ El registro se ha realizado correctamente.");
        this.nombre = "";
        this.correo = "";
        this.contrasena = "";
        this.repetirContrasena = "";
      } else {
        alert("⚠️ Por favor completa todos los campos correctamente.");
      }
    },
  },
};
</script>

<style>
.container {
  max-width: 600px;
}

.centered-label {
  display: block;
  text-align: center;
  font-weight: 600;
  margin-bottom: 0.4rem;
}

.btn-purple {
  background-color: #a68bc2;
  border-color: #967bb6;
  color: white;
  font-weight: 600;
  transition: background-color 0.3s ease;
}

.btn-purple:hover {
  background-color: #967bb6;
  border-color: #7f67a4;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 1.5rem;
}
</style>
