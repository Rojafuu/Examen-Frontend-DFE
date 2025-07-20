<template>
  <div>
    <nav class="navbar">
      <div class="nav-left">
        <span class="logo">Examen Programación FrontEnd</span>
        <router-link to="/" exact-active-class="active">Cálculo de calificaciones</router-link>
        <router-link to="/Formulario" exact-active-class="active">Formulario de Registro</router-link>
        <span class="disabled-tab" title="Sección no disponible">En construcción</span>
      </div>

      <div class="nav-right">
        <input type="text" placeholder="Buscar..." class="search-input" />
        <button class="search-button">Búsqueda</button>
      </div>
    </nav>

    <router-view />
  </div>
</template>

<style>

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 30px;
  background-color: #a68bc2;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.15);
  flex-wrap: wrap;
}

.nav-left {
  display: flex;
  align-items: center;
  gap: 20px;
}
a {
  text-decoration: none;
  color: rgba(240, 230, 255, 0.8); 
  font-weight: 500;
  transition: color 0.2s ease;
}

a.active {
  color: #f0e6ff; 
  font-weight: bold;
}


.disabled-tab {
  color: rgba(255, 255, 255, 0.5);
  opacity: 0.6;
  font-weight: 500;
  cursor: not-allowed;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 10px;
}

.search-input {
  padding: 6px 12px;
  border: none;
  border-radius: 4px;
  outline: none;
  background-color: #f0e6ff; 
  color: #4a4a4a;
  font-weight: 500;
}

.search-button {
  padding: 6px 12px;
  background-color: #8c69b8;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 600;
  transition: background-color 0.3s ease;
}

.search-button:hover {
  background-color: #7a58a3;
}

@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }

  .nav-left,
  .nav-right {
    width: 100%;
    flex-wrap: wrap;
  }

  .search-input {
    width: 60%;
  }

  .search-button {
    width: 30%;
  }
}
</style>