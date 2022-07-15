<script setup>
import { onMounted } from 'vue';

onMounted(() => {
const val1 = document.querySelector("#positivo");
const val2 = document.querySelector("#negativo");
const btn = document.querySelector(".btn");

val1.addEventListener("change", () => {
    if (val1.checked) {
        btn.removeAttribute("disabled");
    }
});

val2.addEventListener("change", () => {
    if (val2.checked) {
        btn.setAttribute("disabled", "");
    }
});

const meses = [
    "Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho",
    "Julho", "Agosto", "Setembro", "Outubro", "Novembro", "Dezembro"
];

function criaOption(value) {
    let option = document.createElement("option");
    option.setAttribute("value", value);
    option.innerHTML = value;
    return option;
}

const mesSelect = document.querySelector(".mes");
meses.forEach((eachMes) => {
    mesSelect.appendChild(criaOption(eachMes));
})

mesSelect.addEventListener("change", (whichMes) => {
    adicionaDia(whichMes.target.value);
})

function contador(inicial, final) {
    let listaDias = [];
    for (let i = inicial; i <= final; i++) {
        listaDias.push(i);
    }
    return listaDias;
}

function adicionaDia(mesValue) {
    const diasSelect = document.querySelector(".dias");
    if (mesValue === "Fevereiro") {
        while (diasSelect.lastChild && diasSelect.childElementCount != 1) {
            diasSelect.removeChild(diasSelect.lastChild);
        }
        let listaDias = contador(1, 29);
        listaDias.forEach((eachDia) => {
            diasSelect.appendChild(criaOption(eachDia));
        })
    } else if (
        mesValue === "Abril" ||
        mesValue === "Junho" ||
        mesValue === "Setembro" ||
        mesValue === "Novembro"
    ) {
        while (diasSelect.lastChild && diasSelect.childElementCount != 1) {
            diasSelect.removeChild(diasSelect.lastChild);
        }
        let listaDias = contador(1, 30);
        listaDias.forEach((eachDia) => {
            diasSelect.appendChild(criaOption(eachDia));
        })
    } else {
        while (diasSelect.lastChild && diasSelect.childElementCount != 1) {
            diasSelect.removeChild(diasSelect.lastChild);
        }
        let listaDias = contador(1, 31);
        listaDias.forEach((eachDia) => {
            diasSelect.appendChild(criaOption(eachDia));
        })
    }

    diasSelect.addEventListener("change", (whichDia) => {
        adicionaAno(whichDia.target.value, mesValue);
    })
}

function adicionaAno(diaValue, mesValue) {
    data = new Date().getFullYear()
    let listaAno = contador(1990, data);
    const anosSelect = document.querySelector(".anos");
    if (diaValue == 29 && mesValue === "Fevereiro") {
        let listaAnoFinal = [];
        listaAno.forEach((eachAno) => {
            if (eachAno % 4 == 0 && eachAno % 100 != 0) {
                listaAnoFinal.push(eachAno);
            }
        })
        while (anosSelect.lastChild && anosSelect.childElementCount != 1) {
            anosSelect.removeChild(anosSelect.lastChild);
        }
        listaAnoFinal.forEach((eachAno) => {
            anosSelect.appendChild(criaOption(eachAno));
        })
    } else {
        while (anosSelect.lastChild && anosSelect.childElementCount != 1) {
            anosSelect.removeChild(anosSelect.lastChild);
        }
        listaAno.forEach((eachAno) => {
            anosSelect.appendChild(criaOption(eachAno));
        })
    }
}
})
</script>

<template>
   <div class="container">
        <div class="row centraliza">
            <form class="card col-8 card shadow rounded-3 pb-3 was-validated">
                <h4 class="card-title text-center pt-2  fw-light">Criar Conta</h4>
                    <div class="form-floating mb-3">
                        <input type="text" class="form-control " id="nome" placeholder="nome" required>
                        <label for="nome">Nome: </label>
                        <div class="invalid-feedback">
                            Por favor, informe um nome de usuário
                        </div>
                    </div>
                    <div class="form-floating mb-3 ">
                        <input type="email" class="form-control " id="email" placeholder="name@example.com" required>
                        <label for="femail">Email: </label>
                        <div class="invalid-feedback">
                            Informe um email válido
                        </div>
                    </div>
                    <div class="form-floating mb-3 ">
                        <input type="password" class="form-control" id="password" placeholder="senha" minlength="6" required>
                        <label for="senha">Senha: </label>
                        <div class="invalid-feedback">
                            A senha é obrigatória e deve conter no mínimo 6 caractéres
                        </div>
                    </div>
                    <div class="form-floating mb-3 ">
                        <input type="password" class="form-control " id="confpassword" placeholder="confsenha" m required>
                        <label for="confpassword">Confirmar Senha: </label>
                        <div class="invalid-feedback">
                            A senha deve ser igual a anterior
                        </div>
                    </div>
                    <div>
                        <h6>Data de nascimento</h6>
                        <span>
                            Isso não sera exibido publicamente.Confirme sua prorpia idade, mesmo sé essa conta for de empresa, de um animal de estimação ou outro
                        </span>
                    </div>
                    <div class="d-flex flex-row justify-content-between">
                        <div class="form-floating w-100">
                            <select class="form-select mes" aria-label="Floating label select example" required>
                            <option value="" disabled selected></option>
                            </select>
                            <label for="floatingSelect">Mes</label>
                        </div>
                        <div class="form-floating w-75">
                            <select class="form-select dias" aria-label="Floating label select example" required>
                            <option value="" disabled selected></option>
                            </select>
                            <label for="floatingSelect1">Dias</label>
                        </div>
                        <div class="form-floating w-100">
                            <select class="form-select anos" aria-label="Floating label select example" required>
                            <option value="" disabled selected></option>
                            </select>
                            <label for="floatingSelect2">Ano</label>
                        </div>
                    </div>
                    <div class="d-flex flex-row infos-checkd">
                        <span>receba e-mails sobre sua atividade no Twitter e recomendações</span>
                        <div class="form-check">
                            <input class="form-check-input" type="checkbox" value="" id="invalidCheck" required>
                        </div>
                    </div>
                    <div class="infos-privacidade">
                        <span>Você concorda com nossos termos, com a Politica de Privacidade e com uso de Coookies ?</span>
                        <div class="d-flex flex-row infos1">
                            <div class="form-check d-flex flex-row">
                                <input type="radio" class="form-check-input" id="negativo" name="radio-stacked" required>
                                <label class="form-check-label" for="negativo">Não</label>
                            </div>

                            <div class="form-check mb-3">
                                <input type="radio" class="form-check-input sim" id="positivo" name="radio-stacked" required>
                                <label class="form-check-label " for="positivo">Sim</label>
                            </div>
                        </div>
                    </div>
                    <div class="d-grid">
                        <button type="submit" disabled class="btn btn-primary btn-lg rounded-pill w-100">Se inscrever</button>
                    </div>



            </form>
        </div>
    </div>
</template>