<template>
  <div class="container mt-5">
    <h2 class="mb-4 text-center">Cálculo de Calificaciones</h2>

    <div class="mb-3">
      <label for="nota1" class="form-label centered-label">Nota 1</label>
      <input type="number" id="nota1" v-model.number="nota1" @input="validarCampo('nota1', nota1)" :class="{'form-control': true, 'is-invalid': errores.nota1}" placeholder="Nota 1" min="10" max="70" />
      <div v-if="errores.nota1" class="text-danger small">{{ errores.nota1 }}</div>
    </div>

    <div class="mb-3">
      <label for="nota2" class="form-label centered-label">Nota 2</label>
      <input type="number" id="nota2" v-model.number="nota2" @input="validarCampo('nota2', nota2)" :class="{'form-control': true, 'is-invalid': errores.nota2}" placeholder="Nota 2" min="10" max="70" />
      <div v-if="errores.nota2" class="text-danger small">{{ errores.nota2 }}</div>
    </div>

    <div class="mb-3">
      <label for="nota3" class="form-label centered-label">Nota 3</label>
      <input type="number" id="nota3" v-model.number="nota3" @input="validarCampo('nota3', nota3)" :class="{'form-control': true, 'is-invalid': errores.nota3}" placeholder="Nota 3" min="10" max="70" />
      <div v-if="errores.nota3" class="text-danger small">{{ errores.nota3 }}</div>
    </div>

    <div class="mb-3">
      <label for="asistencia" class="form-label centered-label">Asistencia %</label>
      <input type="number" id="asistencia" v-model.number="asistencia" @input="validarCampo('asistencia', asistencia)" :class="{'form-control': true, 'is-invalid': errores.asistencia}" placeholder="Asistencia" min="0" max="100"/>
      <div v-if="errores.asistencia" class="text-danger small">{{ errores.asistencia }}</div>
    </div>

  
    <div class="button-container">
      <button class="btn btn-purple w-auto px-4" @click="calcularResultado">Calcular</button>
    </div>


    <div v-if="mensaje" class="mt-4 alert" :class="resultado === 'Aprobado' ? 'alert-success' : 'alert-danger'">
      {{ mensaje }}
    </div>
  </div>
</template>

<script>
export default {
  name: "CalculoCalificaciones",
  data() {
    return {
      nota1: null,
      nota2: null,
      nota3: null,
      asistencia: null,
      resultado: "",
      mensaje: "",
      errores: {
        nota1: null,
        nota2: null,
        nota3: null,
        asistencia: null,
      },
    };
  },
  methods: {
    validarCampo(campo, valor) {
      if (campo.startsWith("nota") && (valor < 10 || valor > 70)) {
        this.errores[campo] = "La nota debe estar entre 10 y 70.";
      } else if (campo === "asistencia" && (valor < 0 || valor > 100)) {
        this.errores[campo] = "La asistencia debe estar entre 0 y 100.";
      } else {
        this.errores[campo] = null;
      }
    },
    calcularResultado() {
      this.validarCampo("nota1", this.nota1);
      this.validarCampo("nota2", this.nota2);
      this.validarCampo("nota3", this.nota3);
      this.validarCampo("asistencia", this.asistencia);

      const hayErrores = Object.values(this.errores).some((e) => e !== null);
      if (
        this.nota1 === null ||
        this.nota2 === null ||
        this.nota3 === null ||
        this.asistencia === null ||
        hayErrores
      ) {
        this.resultado = "Reprobado";
        this.mensaje = "Corrige los errores antes de calcular.";
        return;
      }

      const promedio = this.nota1 * 0.35 + this.nota2 * 0.35 + this.nota3 * 0.3;

      if (promedio >= 40 && this.asistencia >= 80) {
        this.resultado = "Aprobado";
        this.mensaje = `Promedio: ${promedio.toFixed(2)} - Asistencia: ${this.asistencia}% - ¡Aprobado! 🎉`;
      } else {
        this.resultado = "Reprobado";
        this.mensaje = `Promedio: ${promedio.toFixed(2)} - Asistencia: ${this.asistencia}% - Reprobado.`;
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
  margin-bottom: 0.3rem;
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
  color: white;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.alert {
  font-weight: 600;
  text-align: center;
}

.is-invalid {
  border-color: red;
}
</style>
