<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import api from "../services/api";

const register_form = ref({});
const router = useRouter();

async function login(){
  // console.log(register_form.value.email, register_form.value.password );
   try {
      const response = await api.post("/auth/local", {
        identifier: register_form.value.email,
        password: register_form.value.password,
      });

      if(response.data) {
        console.log(router);
        router.push({path: "/"});
      
        return true;
      }

      return false;
    } catch (error) {
      alert("Usuário ou senha incorretos");
    }
}

onMounted(() => {
    let inputEmail = document.getElementById("email");
    let inputPassword = document.getElementById("password");
    let button = document.getElementById("btn");

    document.addEventListener('keyup', function() {
        if (inputEmail.value.length > 0 && inputPassword.value.length > 0) {
            button.removeAttribute("disabled")

        } else {
            button.setAttribute("disabled", "disabled")
        }
    });
});
</script>

<template>
  <div class="container">
    <div class="row centraliza">
      <div class=" col-7 card shadow rounded-3">
        <div class="card-body p-4 p-sm-5">
          <h1 class="card-title text-center mb-5 fw-light fs-5">Entre no tzeet agora mesmo</h1>

          <form class="was-validated" @submit.prevent="login">
            <div class="form-floating mb-3 ">
              <input type="email" class="form-control " id="email" placeholder="name@example.com" required v-model="register_form.email">
              <label for="femail">Email: </label>
              <div class="invalid-feedback">
                Informe um email válido
                  </div>
                        </div>
                        <div class="form-floating mb-3 ">
                            <input type="password" class="form-control" id="password" placeholder="senha" minlength="6" required v-model="register_form.password">
                            <label for="senha">Senha: </label>
                            <div class="invalid-feedback">
                                A senha é obrigatória e deve conter no mínimo 6 caractéres
                            </div>
                        </div>


                        <div class="d-grid">
                            <button type="submit" id="btn" disabled class="w-auto p-2 btn-primary btn-custon" required>Entrar</button>
                            <div class="invalid-feedback">
                                Preencha os campos anteriores
                            </div>
                            <router-link to="/signup">
                              <span>Não tem conta ? Inscreva-se</span>
                            </router-link>
                        </div>

                    </form>
                </div>
            </div>
        </div>
  </div>
</template>

<style>
.container {
  height: 100vh;
}

.centraliza{
    display: flex;
    justify-content: center;
    align-content: center;
    height: 100vh;
  }
</style>