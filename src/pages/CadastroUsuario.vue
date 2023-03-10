<template>
    <div class="q-pa-md">
        <div class="infor-tcc">
            <div>
                <p class="infor-texto">Este é um protótipo do meu TCC, por favor coloque seu melhor email caso queira receber informações adicionais e também relatar sua experiencia.</p>
                <div class="infor-tcc__card" v-if="!msg">
                    <p>Meus dados:</p>
                    <p>maxleandro2@gmail.com</p>
                    <p>(98) 987294634</p>
                    <p>Engenharia de computação (UEMA)</p>
                </div>
                <div class="infor-tcc__card text-alert" v-else>
                    {{ msg }}
                </div>
            </div>
        </div>
        <q-card class="q-pa-md card-cadastro">
            <q-form>
                <q-input v-model="usuario.name" label="Nome" />
                <q-input v-model="usuario.email" label="E-mail" />
                <q-input v-model="usuario.senha" type="password" label="Senha" />
                <div class="btn-cadastro">
                    <q-btn type="submit" color="primary" label="Voltar" @click="login"></q-btn>
                    <q-btn type="submit" color="orange" label="Cadastrar" @click="cadastrar" />
                </div>
            </q-form>
        </q-card>
  </div>
</template>
<script >
import axios from 'axios';
export default {
  name: 'CadastroUsuario',
  data () {
    return {
      usuario: {
        email: '',
        senha: '',
        name: '',
        sexo: ''
      },
      msg: ''
    }
  },
  methods: {
    login() {
        this.$router.push('/login')
    },
    async cadastrar() {
        this.msg = ''
        if( !this.usuario.email || !this.usuario.senha || !this.usuario.name ){
            this.msg = 'Preencha todos os campos.'
            setTimeout(() => {
                this.msg = ''
            }, "4000");
            return;
        }
        try {
        const response = await axios.post('http://localhost:3333/v1/signup', this.usuario)

        if (response.data.status_req === '2') {
          this.msg = 'Ocorreu um erro ou usuário já existe.'
        } else {
            const token = response.data.token
            localStorage.setItem('token', token)
            this.$router.push('/index')
        }
      } catch (error) {
        this.msg = 'Ocorreu um erro.'
      }

      setTimeout(() => {
        this.msg = ''
      }, "4000");
    }
  }
}
</script>
<style>
.card-cadastro {
    margin-top: 8px;
    box-shadow: 0px 0px 4px 0px #a6a6a6;
}
.btn-cadastro {
    display: flex;
    justify-content: space-between;
    gap: 10p;
    margin-top: 20px;
}
.infor-tcc p {
    margin: 0;
    color: #4b4b4b;
    font-size: 13px;
}
.infor-tcc__card {
    background: #e8e8e8;
    border-radius: 10px;
    padding: 9px;
    margin-top: 10px;
    height: 95px;
}
.text-alert {
  text-align: center;
  color: #923005 !important;
  padding-top: 29px;
}
</style>
