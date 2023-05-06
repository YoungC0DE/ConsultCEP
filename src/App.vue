<template>
  <main>
    <div class="main-container">

      <nav class="d-flex flex-column gap-2">
        <span>Informe o CEP:</span>
        <div class="d-flex flex-row search-section">
          <input id="cep" class="form-control rounded-0 rounded-start" type="search" placeholder="Ex: 12345-678" v-maska="'#####-###'" required autofocus autocomplete="off" v-model="CEP" />
          <button class="btn btn-success rounded-0 rounded-end border-0" type="button" v-on:click="consult">
            Consultar
          </button>
        </div>
        <img src="@/assets/detective-img.png" alt="funny icon" width="300" height="200">
      </nav>

      <section>
        <div>
          Logradouro
          <input type="text" class="form-control" placeholder="-----" id="Logradouro" v-model="apiData.logradouro" readonly />
        </div>

        <div>
          Complemento
          <input type="text" class="form-control" placeholder="-----" id="Complemento" v-model="apiData.complemento" readonly />
        </div>

        <div>
          Bairro
          <input type="text" class="form-control" placeholder="-----" id="Bairro" v-model="apiData.bairro" readonly />
        </div>

        <div>
          Localidade
          <input type="text" class="form-control" placeholder="-----" id="Localidade" v-model="apiData.localidade" readonly />
        </div>

        <div>
          UF
          <input type="text" class="form-control" placeholder="-----" id="UF" v-model="apiData.uf" readonly />
        </div>

        <div>
          IBGE
          <input type="text" class="form-control" placeholder="-----" id="IBGE" v-model="apiData.ibge" readonly />
        </div>

        <div>
          GIA
          <input type="text" class="form-control" placeholder="-----" id="GIA" v-model="apiData.gia" readonly />
        </div>

        <div>
          DDD
          <input type="text" class="form-control" placeholder="-----" id="DDD" v-model="apiData.ddd" readonly />
        </div>

        <div>
          SIAFI
          <input type="text" class="form-control" placeholder="-----" id="SIAFI" v-model="apiData.siafi" readonly />
        </div>
      </section>

    </div>
    <footer class="d-flex flex-column align-items-center">
      <span>
        Developed by
        <a href="https://github.com/YoungC0DE" class="text-decoration-none">Rafael Anjos</a>
      </span>
      <span>YoungC0DE</span>
    </footer>
  </main>
</template>

<script>
import axios from "axios";
import { maska } from "maska";
import Swal from "sweetalert2";

export default {
  data() {
    return {
      apiData: {},
      CEP: null,
    };
  },
  directives: { maska },
  methods: {
    consult() {
      if (this.CEP == null || this.CEP.length < 9) {
        Swal.fire({
          title: "CEP inválido",
          text: "Informe um CEP para que possamos prosseguir.",
          icon: "error",
          confirmButtonText: "Ok",
        });
        return;
      }
      axios
        .get(`https://viacep.com.br/ws/${this.CEP}/json`)
        .then(({ data }) => {
          if (data.erro == true) {
            Swal.fire({
              title: "CEP Não encontrado",
              text: "Não encontramos o cep informado, tente novamente com um cep válido.",
              icon: "error",
              confirmButtonText: "Ok",
            });
            return;
          }
          this.apiData = data;
        });
    },
  },
};
</script>
