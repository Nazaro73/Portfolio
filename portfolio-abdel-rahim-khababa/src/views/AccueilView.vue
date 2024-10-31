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
}

h1 {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 2%;
}

h2 {
  margin-top: 2%;
  font-size: 3rem;
  text-align: center;
}

.container {
  width: 100%;
  display: flex;
  justify-content: space-around;
  height: 500px;
  gap: 10px;
}

.carousel-item {
  flex: 1; /* Prend de l'espace disponible */
  border-radius: 0.5rem;
  transition: 0.5s ease-in-out;
  cursor: pointer;
  box-shadow: 1px 5px 15px #1e0e3e;
  position: relative;
  overflow: hidden;
  text-decoration: none; /* Enlève le soulignement du lien */
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
  font-size: 1.5rem;
  color: #fff;
  display: flex;
  align-items: center;
  padding: 15px;
  opacity: 0;
  flex-direction: column;
  height: 100%;
  justify-content: flex-end;
  background: rgb(2, 2, 46);
  background: linear-gradient(
    0deg,
    rgba(2, 2, 46, 0.6755077030812324) 0%,
    rgba(255, 255, 255, 0) 100%
  );
  transform: translatey(100%);
  transition: opacity 0.5s ease-in-out, transform 0.5s 0.2s;
  visibility: hidden;
}

.carousel-item:hover {
  flex: 2;
  box-shadow: 1px 3px 15px #7645d8;
  transform: translateY(-30px);
}

.carousel-item:hover .content {
  opacity: 1;
  transform: translateY(0%);
  visibility: visible;
}

.container .content span {
  display: block;
  margin-top: 5px;
  font-size: 1.2rem;
}
</style>
