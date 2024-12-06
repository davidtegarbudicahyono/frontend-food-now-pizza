<template>
    <header class="web-header">
      <nav class="navbar navbar-expand-lg navbar-dark bg-transparent">
        <div class="container">
          <!-- Logo -->
            <img src="@/assets/img/logo.svg" alt="Logo" class="d-inline-block align-text-top">
          <!-- Toggle button for mobile view -->
            <button
                class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarNav"
                aria-controls="navbarNav"
                aria-expanded="false"
                aria-label="Toggle navigation"
            >
            <span class="navbar-toggler-icon"></span>
            </button>
          <!-- Navigation links -->
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
              <li class="nav-item">
                <a class="nav-link" href="#">Home</a>
              </li>
              <li class="nav-item">
                <a class="nav-link " href="#">Order</a>
              </li>
              <li class="nav-item">
                <a class="nav-link " href="#">About</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Blog</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Contact us</a>
              </li>
            </ul>
          </div>
          <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
            <ul class="navbar-nav ms-auto align-items-center">
              <li class="nav-item">
                <a class="btn btn-login ms-2 fs-5" href="#">Login</a>
              </li>
              <li class="nav-item">
                <a class="btn btn-register ms-2 fs-5" href="#">Register</a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
      <!-- Hero Section -->
      <div class="hero-section">
        <h1>Pizza order</h1>
      </div>
    </header>
</template>
  
<script>

export default {
  name: "WebHeader",
};

</script>
  
<style scoped>

.navbar-NAvigationBar {
    margin-left: 70px;
  }

.web-header {
  background-image: url("@/assets/img/hero.png");
  min-width: 100px;
  height: 100vh;
  background-size: cover;
  margin-bottom: 20px;
}

.navbar {
  padding: 1rem 0;
}

.nav-link {
  color: white;
  font-size: 20px;
}

.nav-link:hover {
  color: #fa921a;
}

.hero-section {
  margin-top: 250px;
  margin-bottom: auto;
  text-align: center;
  color: #fa921a;
}

.hero-section h1 {
  font-size: 4rem;
}

.hero-section p {
  font-size: 1.2rem;
}

.navbar-nav .nav-item .btn {
  margin-bottom: 0;
}

/* Tombol Login */
.btn-login {
  background-color: transparent; 
  color: white; 
  border:none;
}

.btn-login:hover {
  color: #fa921a;
}

/* Tombol Register */
.btn-register {
  background-color:#fa921a; 
  color: white;
}

.btn-register:hover {
  background-color: rgb(218, 133, 6); 
  color:white;
}


@media (max-width: 768px) {
  .navbar-nav {
    flex-direction: column; 
    gap: 10px;
  }

  .navbar-nav .nav-item .btn {
    width: 100%; 
    margin-bottom: 10px; 
  }

  .navbar-nav .nav-item:last-child .btn {
    margin-bottom: 0; 
  }
}



</style>
  