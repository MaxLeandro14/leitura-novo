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
    <q-card class="q-pa-md card-login">
      <q-form>
        <q-input v-model="usuario.email" type="email" label="Email"></q-input>
        <q-input v-model="usuario.password" type="password" label="Senha"></q-input>
        <div class="btn-login">
          <q-btn type="submit" color="orange" label="Cadastrar" @click="cadastrar"></q-btn>
          <q-btn type="submit" color="primary" label="Login" @click="login"></q-btn>
        </div>
      </q-form>
    </q-card>
  </div>
</template>

<script>
import { Buffer } from 'buffer';
import axios from 'axios';
export default {
  name: 'LoginPage',
  data () {
    return {
      usuario: {
        email: '',
        password: ''
      },
      msg: ''
    }
  },
  methods: {
    cadastrar() {
      this.$router.push('/cadastro')
    },
    async login() {
      this.msg = ''
      if (!this.usuario.email || !this.usuario.password) {
        this.msg = 'Preencha todos os campos.'
        setTimeout(() => {
          this.msg = ''
        }, "4000");
        return
      }
      try {
        const response = await axios.get('http://localhost:3333/v1/login', {
          headers: {
            Authorization: `Basic ${Buffer.from(`${this.usuario.email}:${this.usuario.password}`).toString('base64')}`
          }
        })
        if (response.data.status_req === '2') {
          this.msg = 'Email ou Senha incorreta.'
        } else {
          const token = response.data.token
          localStorage.setItem('token', token)
          this.$router.push('/index')
        }
      } catch (error) {
        this.msg = 'Ocooreu um erro ao acessar sua conta!'
      }
      setTimeout(() => {
        this.msg = ''
      }, "4000");
    }
  }
}
</script>
<style>
.card-login {
    margin-top: 8px;
    box-shadow: 0px 0px 4px 0px #a6a6a6;
}
.btn-login {
  display: flex;
  justify-content: space-between;
  gap: 5px;
  margin-top: 8px;
}
.infor-tcc p {
    margin: 0;
    color: #4b4b4b;
    font-size: 13px;
}
.infor-texto {
    text-align: center;
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
  padding-top: 35px;
}
</style>

