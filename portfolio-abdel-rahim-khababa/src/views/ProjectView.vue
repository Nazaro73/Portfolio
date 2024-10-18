<template>
  <div class="body">
  <div class="all">
  <header>
    <h1>Mes Projets</h1>
    <p>
      Bienvenue dans la section où je présente certains de mes projets. Si vous
      souhaitez jeter un œil à mon GitHub, vous pouvez consulter mes autres
      réalisations à l'adresse suivante :
      <a href="https://github.com/Nazaro73" target="_blank">Mon GitHub</a>.
      Cependant, certains projets, notamment ceux réalisés pour des entreprises,
      ne sont pas disponibles sur ce compte.
    </p>
  </header>

  <!-- Premier projet : Site vitrine de massage -->
  <section>
    <h2>Projet 1 : Site vitrine de massage</h2>
    <a href="https://www.eden-headspa.com/" target="_blank"><img src="../assets/img/projeden.png" alt=""></a>
    <p>
      Ce projet consiste à créer un site vitrine pour un professionnel du
      massage avec l'implémentation d'un Google Agenda pour la prise de
      rendez-vous en ligne. J'ai moi-même configuré l'agenda Google et réalisé
      le site en suivant un design fourni par le client. J'ai effectué plusieurs
      itérations de modifications pour respecter les demandes spécifiques du
      client en matière de design. Ce projet a été réalisé pour une personne que
      je connais.
    </p>

    <!-- Bouton "T" avec les icônes technologiques en dessous -->
    <div class="tech-circle">T</div>
    <div class="tech-icons">
      <img src="../assets/svg/git.svg" alt="Git">
      <img src="../assets/svg/vuejs.svg" alt="Vue.js">
    </div>
  </section>

  <!-- Deuxième projet : Leads.fr -->
  <section>
    <h2>Projet 2 : Leads.fr (Confidentiel)</h2>
    <img src="../assets/img/projKirby.png" alt="">
    <p>
      Le projet <strong>Leads.fr</strong> a été développé lors de mon
      alternance. Il s'agit d'un outil de data visualisation pour suivre les
      retours des leads livrés par mon entreprise. J'ai travaillé sur ce projet
      de A à Z, créant une API Express pour le back-end et utilisant Vue.js pour
      le front-end.
    </p>
    <p>
      Ce projet était essentiel pour améliorer la qualité des leads livrés et
      pour permettre à l'équipe marketing de prendre des décisions éclairées.
      J'ai travaillé seul sur la majeure partie du projet, avec l'aide
      ponctuelle d'un développeur expérimenté. Cela m'a permis de développer mes
      compétences en communication avec les clients et en gestion de projet.
    </p>

    <!-- Bouton "T" avec les icônes technologiques en dessous -->
    <div class="tech-circle">T</div>
    <div class="tech-icons">
      <img src="../assets/svg/vuejs.svg" alt="Vue.js">
      <img src="../assets/svg/express.svg" alt="Express.js">
      <img src="../assets/svg/git.svg" alt="Git">
      <img src="../assets/svg/docker.svg" alt="Docker">
    </div>
  </section>

  <!-- Troisième projet : MyDigitalProject -->
  <section>
    <h2>Projet 3 : MyDigitalProject (Projet non hebergé)</h2>
    <a href="https://github.com/Nazaro73/GreenTravelApp" target="_blank"><img src="../assets/img/projmdp.png" alt=""></a>
    <p>
      Ce projet a été réalisé dans le cadre de mes études à MyDigitalSchool. Il
      s'agit d'une application mobile de planification de voyage développée avec
      Flutter. Le back-end a été réalisé avec une API Express.
    </p>
    <p>
      Ce projet m'a permis d'apprendre à utiliser Flutter et de collaborer avec
      des étudiants d'autres sections comme le marketing et le design.
      L'application permet d'ajouter des participants à un voyage et d'organiser
      plusieurs aspects d'une expédition. Bien que le projet n'ait pas été
      entièrement terminé, c'était une expérience enrichissante pour apprendre
      le développement d'applications mobiles.
    </p>

    <!-- Bouton "T" avec les icônes technologiques en dessous -->
    <div class="tech-circle">T</div>
    <div class="tech-icons">
      <img src="../assets/svg/flutter.svg" alt="Flutter">
      <img src="../assets/svg/express.svg" alt="Express.js">
      <img src="../assets/svg/git.svg" alt="Git">
    </div>
  </section>

</div>
</div>
</template>


<script>
export default {
  name: 'ProjectView'
};
</script>

<style scoped>
/* Import arcade-style font from Google Fonts */
/* Import police Ubuntu Mono */
@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Mono&display=swap');

.body{
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('../assets/img/background.jpg'); /* Chemin vers ton image */
      background-repeat: repeat; /* Répète l'image sur toute la page */
      background-size: 700px;
  
}


/* Style global */
.all {
  max-width: 800px;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Ubuntu Mono', monospace; /* Police développeur */
    color: #2b2b2b; /* Couleur de texte douce */
    background-color: #2b2b2b;
}



html, body {
    background-color: #1e1e1e; /* Fond sombre mais pas trop contrasté */
    line-height: 1.6; /* Meilleure lisibilité */
    padding: 20px;
}

/* Header styling */
header {
    text-align: center;
    padding: 20px;
    background-color: #2c2c2c; /* Fond légèrement plus foncé */
    border-bottom: 2px solid #444; /* Lignes subtiles pour la séparation */
}

header h1 {
    font-size: 2rem;
    margin-bottom: 10px;
    color: #e0e0e0; /* Blanc doux */
}

header p {
    font-size: 1rem;
    color: #bbbbbb; /* Gris plus doux pour les paragraphes */
}

/* Style des sections de projets */
section {
    margin: 30px auto;
    padding: 20px;
    width: 90%;
    max-width: 1000px;
    background-color: #e0e0e0; /* Couleur sombre subtile pour le fond des sections */
    border-radius: 10px; /* Coins légèrement arrondis */
    border: 1px solid #444; /* Bordure discrète */
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.3); /* Légère ombre pour donner de la profondeur */
    text-align: center;
    position: relative; /* Nécessaire pour le bouton circulaire "T" */
}

/* Style des titres de projets */
section h2 {
    font-size: 1.5rem;
    color: #2b2b2b;
    margin-bottom: 20px;
}

/* Images des projets */
section img {
    display: block;
    margin: 0 auto 20px;
    width: 80%;
    max-width: 500px; /* Ajustement de la taille */
    border-radius: 10px;
    border: 2px solid #444; /* Bordure subtile pour les images */
}

/* Texte de présentation des projets */
section p {
    font-size: 1rem;
    line-height: 1.6;
    margin-bottom: 20px;
    color: #222222; /* Couleur de texte légèrement atténuée */
    text-align: justify;
}

/* Bouton "T" (Technologie) */
.tech-circle {
    position: absolute;
    bottom: 20px;
    right: 20px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #3a3a3a; /* Fond sombre et neutre */
    display: flex;
    align-items: center;
    justify-content: center;
    color: #2b2b2b;
    font-size: 1rem;
    cursor: pointer;
    transition: transform 0.3s ease, background-color 0.3s ease;
}

.tech-circle:hover {
    background-color: #444;
    transform: scale(1.1);
}

/* Icônes SVG des technologies */
section img[src$=".svg"] {
    width: 30px;
    height: 30px;
    margin: 5px;
    transition: filter 0.3s ease;
}

/* Animation SVG lors du hover sur le bouton "T" */
.tech-circle:hover + .tech-icons {
    opacity: 1;
    transform: translateY(0);
}

.tech-icons {
    position: absolute;
    bottom: 20px; /* Aligner sur le même niveau vertical que le bouton "T" */
    left: 27vw; /* Les icônes apparaîtront à gauche du bouton "T" */
    display: flex;
    flex-wrap: wrap;
    opacity: 0;
    transform: translateY(10px);
    transition: opacity 0.3s ease, transform 0.3s ease;
}

.tech-icons img {
    width: 30px;
    height: 30px;
    margin: 5px;
}


</style>