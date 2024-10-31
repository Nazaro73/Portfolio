<template>
    <div class="container-main">
    <div class="contact-container">
      <h2 class="contact-title">Get in touch</h2>
      <h1 class="contact-header">Contactez Moi</h1>
      <div class="contact-content">
        <div class="contact-options">
          <div class="contact-option">
            <div class="icon">📧</div>
            <h3>Email</h3>
            <p><a href="mailto:abdel-rahim.khababa@hotmail.com">Un mail par ici →</a></p>
          </div>
          <div class="contact-option">
            <div class="icon">💬</div>
            <h3>Whatsapp</h3>
            <p><a href="https://wa.me/33+766324045">Un SMS par là →</a></p>
          </div>
          <div class="contact-option">
            <div class="icon">💬</div>
            <h3>Linkedin</h3>
            <p><a href="https://wa.me/33+766324045">Ou un Linkedin par ici →</a></p>
          </div>
        </div>
  
        <form class="contact-form">
          <h2>Des questions ?</h2>
          <div class="form-group">
            <label for="name">Nom</label>
            <input type="text" id="name" placeholder="Votre nom" />
          </div>
          <div class="form-group">
            <label for="email">Mail</label>
            <input type="email" id="email" placeholder="Votre mail" />
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" placeholder="Votre message"></textarea>
          </div>
          <button type="submit" class="submit-btn">Envoyer</button>
        </form>
      </div>
    </div>
</div>
  </template>
  
  <script>
  export default {
    name: 'ContactForm',
    methods: {
      // Placeholder for form submission logic
      handleSubmit() {
        alert('Message sent!');
      },
    },
  };
  </script>
  
  <style scoped>
   .container-main {
    
   } 

  .contact-container {
    border-radius: 10%;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #fff;
    background-color: #111;
    padding: 2rem;
  }
  
  .contact-title {
    font-size: 1rem;
    color: #999;
    text-align: center;
  }
  
  .contact-header {
    font-size: 2rem;
    color: #4466ff;
    text-align: center;
    margin-bottom: 1.5rem;
  }
  
  .contact-content {
    display: flex;
    gap: 2rem;
    width: 100%;
    max-width: 800px;
  }
  
  .contact-options {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  
  .contact-option {
    background-color: #1b2341;
    padding: 1.5rem;
    border-radius: 10px;
    text-align: center;
    color: #fff;
  }
  
  .contact-option .icon {
    font-size: 2rem;
    margin-bottom: 0.5rem;
  }
  
  .contact-option h3 {
    font-size: 1.25rem;
    margin: 0;
  }
  
  .contact-option p a {
    color: #4466ff;
    text-decoration: none;
  }
  
  .contact-form {
    flex: 1;
    background-color: #111;
    padding: 1.5rem;
    border-radius: 10px;
  }
  
  .contact-form h2 {
    color: #fff;
    margin-bottom: 1rem;
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
    margin-bottom: 1rem;
  }
  
  .form-group label {
    color: #bbb;
    margin-bottom: 0.5rem;
  }
  
  .form-group input,
  .form-group textarea {
    padding: 0.5rem;
    background-color: transparent;
    border: 1px solid #4466ff;
    border-radius: 5px;
    color: #fff;
    font-size: 1rem;
  }
  
  textarea {
    resize: none;
    height: 100px;
  }
  
  .submit-btn {
    background-color: #4466ff;
    border: none;
    color: #fff;
    padding: 0.75rem 1.5rem;
    border-radius: 5px;
    cursor: pointer;
    font-size: 1rem;
  }
  
  .submit-btn:hover {
    background-color: #3355dd;
  }
  </style>
  