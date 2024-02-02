<template>
  <div class="form-container">
    <form @submit="onSubmit" class="form">
      <div class="form-group">
        <label for="name">Imię:</label>
        <input v-model="name" v-bind="nameAttrs" name="name" type="name" />
        <span class="error" v-if="errors.name">Imię jest wymagane</span>
      </div>
      <div class="form-group">
        <label for="email">Email:</label>
        <input v-model="email" v-bind="emailAttrs" name="email" type="email" />
        <span class="error"  v-if="errors.email">Nieprawidłowy format adresu e-mail</span>
      </div>

      <div class="form-group">
        <label for="passw">Hasło:</label>
        <input
          v-model="passw"
          v-bind="passwAttrs"
          name="passw"
          type="password"
        />
        <span class="error" v-if="errors.passw">Hasło musi zawierać conajmniej 6 znaków</span>
      </div>

      <button type="submit" class="submit-button">Zatwierdź</button>
    </form>
  </div>
</template>

<script setup>
import { useForm } from "vee-validate";
import * as yup from "yup";

const schema = yup.object({
  name: yup.string().required(),
  email: yup.string().email().required(),
  passw: yup.string().min(6).required(),
});

const { defineField, errors, handleSubmit } = useForm({
  validationSchema: schema,
});

const [name, nameAttr] = defineField("name");
const [email, emailAttrs] = defineField("email");
const [passw, passwAttrs] = defineField("passw");

const onSubmit = handleSubmit((values) => {
  alert(JSON.stringify(values, null, 2));
});
</script>

<style scoped>
.form-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Set to 100% of the viewport height for vertical centering */
}

.form {
  width: 500px; /* Adjust the width as needed */
  height: 500px;
  background-color: rgb(203, 203, 203);
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.form-group {
  min-width: 70%;
  margin-bottom: 15px;
  display: flex;
  flex-direction: column; /* Adjust to stack label, input, and error vertically */
}

label {
  display: block;
  margin-bottom: 5px;
}

.error {
  color: red;
  margin-top: 5px; /* Add margin at the top to separate from the input */
}

.submit-button {
  background-color: #4caf50; /* Green background */
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px; /* Add margin at the top to separate from the last input */
}

.submit-button:hover {
  background-color: #45a049; /* Darker green on hover */
}
</style>
