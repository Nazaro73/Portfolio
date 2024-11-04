<template>
  <div class="container-main">
    <h1>Salut ! Je suis Abdel-Rahim KHABABA</h1>
    
    <nav>
      <div class="container">
        <router-link to="/profile" class="carousel-item">
          <div class="content">
            <h2>Mon Profile</h2>
            <span>Section Profile</span>
          </div>
        </router-link>
        <router-link to="/project" class="carousel-item">
          <div class="content">
            <h2>Mes Projets</h2>
            <span>Section Projets</span>
          </div>
        </router-link>
        <router-link to="/contact" class="carousel-item">
          <div class="content">
            <h2>Contact</h2>
            <span>Section Contact</span>
          </div>
        </router-link>
      </div>
    </nav>

    <h2>Je suis un Développeur Full Stack</h2>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu+Mono&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container-main {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-image: url('../assets/img/background.jpg');
  background-repeat: repeat;
  background-size: cover;
  color: whitesmoke;
  font-family: "Ubuntu Mono", monospace;
  padding: 20px;
}

h1 {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 2%;
}

h2 {
  margin-top: 2%;
  font-size: 2rem;
  text-align: center;
}

.container {
  width: 100%;
  display: flex;
  justify-content: space-around;
  gap: 10px;
  flex-wrap: wrap;
}

.carousel-item {
  flex: 1 1 30%; /* Par défaut, chaque item occupe environ 30% */
  min-width: 250px; /* Largeur minimale pour chaque item */
  height: 500px; /* Hauteur adaptée pour les petits écrans */
  border-radius: 0.5rem;
  transition: 0.5s ease-in-out;
  cursor: pointer;
  box-shadow: 1px 5px 15px #1e0e3e;
  position: relative;
  overflow: hidden;
  text-decoration: none; /* Enlève le soulignement du lien */
  display: flex;
  align-items: flex-end;
}

.carousel-item:nth-of-type(1) {
  background: url("../assets/img/history.jpg") no-repeat 50% / cover;
}
.carousel-item:nth-of-type(2) {
  background: url("../assets/img/passion.jpg") no-repeat 50% / cover;
}
.carousel-item:nth-of-type(3) {
  background: url("../assets/img/project.jpg") no-repeat 50% / cover;
}
.carousel-item:nth-of-type(4) {
  background: url("../assets/img/ia.jpg") no-repeat 50% / cover;
}

.container .content {
  font-size: 1.2rem;
  color: #fff;
  display: flex;
  align-items: center;
  padding: 15px;
  opacity: 0;
  flex-direction: column;
  height: 100%;
  justify-content: flex-end;
  background: linear-gradient(
    0deg,
    rgba(2, 2, 46, 0.7) 0%,
    rgba(255, 255, 255, 0) 100%
  );
  transform: translateY(100%);
  transition: opacity 0.5s ease-in-out, transform 0.5s 0.2s;
  visibility: hidden;
}

.carousel-item:hover {
  flex: 1.5; /* Ajuste la taille en survol pour être plus réactif */
  box-shadow: 1px 3px 15px #7645d8;
  transform: translateY(-20px);
}

.carousel-item:hover .content {
  opacity: 1;
  transform: translateY(0%);
  visibility: visible;
}

.container .content span {
  display: block;
  margin-top: 5px;
  font-size: 1rem;
}

/* Media Queries pour les écrans moyens et petits */
@media (max-width: 1024px) {
  h1, h2 {
    font-size: 2rem;
  }

  .container {
    flex-direction: column;
    align-items: center;
  }

  .carousel-item {
    flex: 1 1 80%; /* Occupe plus d'espace sur les écrans moyens */
    height: 250px;
  }
}

@media (max-width: 768px) {
  h1 {
    font-size: 1.8rem;
  }

  h2 {
    font-size: 1.5rem;
  }

  .carousel-item {
    flex: 1 1 100%; /* Chaque item occupe toute la largeur */
    height: 200px;
  }

  .container .content {
    font-size: 1rem;
  }
}
</style>
