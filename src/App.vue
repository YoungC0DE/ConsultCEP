<template>

  <nav class="bg-dark">
    <form class="d-flex" role="search">
      <span class="text-white">Informe um CEP:</span>
      <input id="cep" class="form-control me-2" type="search" placeholder="Ex: 12345-678" aria-label="Search"
        v-model="cep">
      <button class="btn btn-outline-success" type="submit" v-on:click="consult">Consultar</button>
    </form>
  </nav>

  <main>
    <section>
      <div class="duo-blocks">
        <div>
          Logradouro
          <input type="text" class="form-control" aria-label="Sizing example input" id="Logradouro" v-model="logradouro"
            readonly>
        </div>

        <div>
          Complemento
          <input type="text" class="form-control" aria-label="Sizing example input" id="Complemento"
            v-model="complemento" readonly>
        </div>
      </div>

      <div class="duo-blocks">
        <div>
          Bairro
          <input type="text" class="form-control" aria-label="Sizing example input" id="Bairro" v-model="bairro"
            readonly>
        </div>

        <div>
          Localidade
          <input type="text" class="form-control" aria-label="Sizing example input" id="Localidade" v-model="localidade"
            readonly>
        </div>
      </div>

      <div class="duo-blocks">
        <div>
          UF
          <input type="text" class="form-control" aria-label="Sizing example input" id="UF" v-model="uf" readonly>
        </div>

        <div>
          IBGE
          <input type="text" class="form-control" aria-label="Sizing example input" id="IBGE" v-model="ibge" readonly>
        </div>
      </div>


      <div class="three-blocks">
        <div>
          GIA
          <input type="text" class="form-control" aria-label="Sizing example input" id="GIA" v-model="gia" readonly>
        </div>

        <div>
          DDD
          <input type="text" class="form-control" aria-label="Sizing example input" id="DDD" v-model="ddd" readonly>
        </div>

        <div>
          SIAFI
          <input type="text" class="form-control" aria-label="Sizing example input" id="SIAFI" v-model="siafi" readonly>
        </div>
      </div>

    </section>
  </main>

</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      cep: '',
      logradouro: '',
      complemento: '',
      bairro: '',
      localidade: '',
      uf: '',
      ibge: '',
      gia: '',
      ddd: '',
      siafi: ''
    }
  },
  methods: {
    consult() {
      console.log(this.cep)
      axios
        .get(`https://viacep.com.br/ws/${this.cep}/json`)
        .then(({data}) => {
          this.bairro = data.bairro
          this.logradouro = data.logradouro
          this.complemento = data.complemento
          this.localidade = data.localidade
          this.uf = data.uf
          this.ibge = data.ibge
          this.gia = data.gia
          this.ddd = data.ddd
          this.siafi = data.siafi
        })
    }
  }
}
</script>