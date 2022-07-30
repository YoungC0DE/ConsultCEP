<template>

  <nav class="bg-dark">
    <form class="d-flex" role="search">
      <span class="text-white">Informe um CEP:</span>
      <input id="cep" class="form-control me-2" type="search" placeholder="Ex: 12345-678" v-maska="'#####-###'"
        aria-label="Search" v-model="Dados.cep">
      <button class="btn btn-outline-success" type="submit" v-on:click.prevent="consult">Consultar <i
          class="bi bi-search"></i></button>
    </form>
  </nav>

  <main>
    <section>
      <div class="duo-blocks">
        <div>
          Logradouro
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="Logradouro"
            v-model="Dados.logradouro" readonly>
        </div>

        <div>
          Complemento
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="Complemento"
            v-model="Dados.complemento" readonly>
        </div>
      </div>

      <div class="duo-blocks">
        <div>
          Bairro
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="Bairro"
            v-model="Dados.bairro" readonly>
        </div>

        <div>
          Localidade
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="Localidade"
            v-model="Dados.localidade" readonly>
        </div>
      </div>

      <div class="duo-blocks">
        <div>
          UF
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="UF"
            v-model="Dados.uf" readonly>
        </div>

        <div>
          IBGE
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="IBGE"
            v-model="Dados.ibge" readonly>
        </div>
      </div>


      <div class="three-blocks">
        <div>
          GIA
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="GIA"
            v-model="Dados.gia" readonly>
        </div>

        <div>
          DDD
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="DDD"
            v-model="Dados.ddd" readonly>
        </div>

        <div>
          SIAFI
          <input type="text" class="form-control" aria-label="Sizing example input" placeholder="-----" id="SIAFI"
            v-model="Dados.siafi" readonly>
        </div>
      </div>

    </section>
  </main>
  <iframe
    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d25061235.470727414!2d-53.29014935068654!3d-14.970935823514925!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x9c59c7ebcc28cf%3A0x295a1506f2293e63!2sBrasil!5e0!3m2!1spt-BR!2sbr!4v1659142100472!5m2!1spt-BR!2sbr"
    width="100%" height="300" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade">
  </iframe>
</template>

<script>
import axios from 'axios'
import { maska } from 'maska'

export default {
  data() {
    return {
      Dados: {}
    }
  },
  directives: { maska },
  methods: {
    consult() {
      console.log(this.cep)
      axios
        .get(`https://viacep.com.br/ws/${this.Dados.cep}/json`)
        .then(({ data }) => {
          this.Dados.bairro = data.bairro
          this.Dados.logradouro = data.logradouro
          this.Dados.complemento = data.complemento
          this.Dados.localidade = data.localidade
          this.Dados.uf = data.uf
          this.Dados.ibge = data.ibge
          this.Dados.gia = data.gia
          this.Dados.ddd = data.ddd
          this.Dados.siafi = data.siafi
        })
    }
  }
}
</script>
