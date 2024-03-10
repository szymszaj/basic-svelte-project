<script>
  import { onMount } from 'svelte';

  let username = '';
  let password = '';
  let password2 = '';
  let email = '';
  let popupVisible = false;

  const showError = (input, msg) => {
    input.classList.add('error');
    const errorMsg = input.parentElement.querySelector('.error-text');
    errorMsg.textContent = msg;
  };

  const clearError = input => {
    input.classList.remove('error');
    const errorMsg = input.parentElement.querySelector('.error-text');
    errorMsg.textContent = '';
  };

  const checkForm = () => {
    const inputs = document.querySelectorAll('.form-box input');
    inputs.forEach(input => {
      if (input.value === '') {
        showError(input, input.placeholder);
      } else {
        clearError(input);
      }
    });
  };

  const checkLength = (input, min) => {
    if (input.value.length < min) {
      showError(input, `${input.previousElementSibling.innerText.slice(0, -1)} składa się z min. ${min} znaków`);
    }
  };

  const checkPassword = () => {
    if (password !== password2) {
      showError(document.getElementById('password2'), 'Hasła do siebie nie pasują.');
    }
  };

  const checkEmail = () => {
    const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    if (!re.test(email)) {
      showError(document.getElementById('email'), 'E-mail jest niepoprawny');
    }
  };

  const checkErrors = () => {
    const errorInputs = document.querySelectorAll('.form-box.error input');
    if (errorInputs.length === 0) {
      popupVisible = true;
    }
  };

  const clearForm = () => {
    username = '';
    password = '';
    password2 = '';
    email = '';
    const inputs = document.querySelectorAll('.form-box input');
    inputs.forEach(input => clearError(input));
  };

  const handleSubmit = () => {
    checkForm();
    checkLength(document.getElementById('username'), 3);
    checkLength(document.getElementById('password'), 8);
    checkPassword();
    checkEmail();
    checkErrors();
  };

  onMount(() => {
    const sendBtn = document.querySelector('.send');
    const clearBtn = document.querySelector('.clear');
    const popup = document.querySelector('.popup');

    sendBtn.addEventListener('click', e => {
      e.preventDefault();
      handleSubmit();
    });

    clearBtn.addEventListener('click', e => {
      e.preventDefault();
      clearForm();
    });

    popup.addEventListener('click', () => {
      popupVisible = false;
    });
  });
</script>
  
<style lang="css">
  @import './Register.css';
</style>

<div class="wrapper">
  <form>
    <h1>Zarejestruj się!</h1>

    <div class="form-box">
      <label for="username">Nazwa użytkownika:</label>
      <input type="text" id="username" placeholder="Podaj nazwę użytkownika">
      <p class="error-text">error</p>
    </div>

    <div class="form-box">
      <label for="password">Hasło:</label>
      <input type="password" id="password" placeholder="Podaj hasło">
      <p class="error-text">error</p>
    </div>
    <div class="form-box">
      <label for="password2">Powtórz hasło:</label>
      <input type="password" id="password2" placeholder="Powtórz hasło">
      <p class="error-text">error</p>
    </div>
    <div class="form-box">
      <label for="email">Adres e-mail:</label>
      <input type="email" id="email" placeholder="Podaj adres mailowy">
      <p class="error-text">error</p>
    </div>

    <div class="control-buttons">
      <button class="clear">Wyczyść</button>
      <button class="send">Wyślij</button>
    </div>

    <div class="popup">
      <p>Formularz został poprawnie wysłany!</p>
      <button class="close">Zamknij</button>
    </div>
  </form>
</div>
