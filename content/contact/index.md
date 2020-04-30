+++
date = "2020"
title = "Contact"
+++

<script src="https://www.google.com/recaptcha/api.js?render=6Lf-MfAUAAAAAE4dwSezxCqvNloSgnV3wdHcXJUN"></script>

<script>
grecaptcha.ready(function() {
    grecaptcha.execute('6Lf-MfAUAAAAAE4dwSezxCqvNloSgnV3wdHcXJUN', {action: 'contact'});
});
</script>

<style>

.grecaptcha-badge {
  bottom: 60px !important;
}
  #contactForm {
      margin: 0 auto;
}

  #contactForm input, textarea {
      letter-spacing: 2px;
      font: 200 1em/1.1em 'Helvetica Neue', sans-serif;
      
      color: #E7EDF1;
      background-color: RGBA(204, 204, 204, .1);
    
      outline: none; border: none;
   
      display:block;
      margin: 0 auto;
      padding: 1em;
      width: 90%;
      max-width: 400px;
 }

#contactForm textarea {
  height: 150px;
}

#contactForm *:focus {
   background-color: #F92672;
}

#contactForm *:hover {
   background-color: #F92672;
}

::-webkit-input-placeholder {
      color: #E7EDF1;
}

:-moz-placeholder { /* Firefox 18- */
      color: #E7EDF1; 
}

::-moz-placeholder {  /* Firefox 19+ */
    color: #E7EDF1; 
}

:-ms-input-placeholder {  
       color: #E7EDF1;
}
</style>
<form action="/thankyou" data-netlify="true" id="contactForm" onsubmit="return validate()"  method="post" netlify>
<!-- <p style="visibilty: hidden">
  <label>Don't fill this out if you're human:</label><input name=bot-field>
</p> -->
  <input class="formInput" type="text" id="name" name="name" autocorrect="off" placeholder="Name"/>
  <input class="formInput" type="email" name="email" id="email" autocapitalize="off" autocorrect="off" placeholder="Email"/>
  <textarea class="formInput" name="message" id="message" placeholder="Message"></textarea>
  
  <br>
    <input class="submitForm" type="reset" value="Clear your message" />
    <br/>
    <br>
    <div data-netlify-recaptcha></div>
    <strong><input class="submitForm" type="submit" value="Send"/></strong>
          
</form>