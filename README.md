# Nuxt JS - WhatsApp Card

![@karytonn.dev](https://media-exp1.licdn.com/dms/image/D4D12AQE8EfAx1Ra6Sg/article-cover_image-shrink_720_1280/0/1669902162582?e=1675296000&v=beta&t=PSm-62l2pUqMfOTNjMsarXh66Y0nnIUxoUzZ0yizU88 "@karytonn.dev")

Seja para conversão do **GoogleADS** ou simplesmente fornecer um meio de contato rápido para clientes, ter um botão de **WhatsApp** integrado ao site é indispensável nos dias de hoje.

Por mais que pareça simples, fazer isso de forma que se adapte aos mais diversos casos de uso pode levar tempo, sendo assim, aproveito para compartilhar meu template que desenvolvi em **VueJS** / **NuxtJS**.

---

**Para esse template iremos utilizar os seguintes recursos:**

- Projeto em Vue JS ou Nuxt JS (suponho que já tenha)
- Tailwind CSS - Estilização
- Animate CSS - Animação (opcional)

*Se desejar utilizar somente a estilização do componente, fique a vontade para copiar a parte do HTML/CSS, que inclusive, já vou deixar separadinho [aqui](https://github.com/Karytonn/nuxtjs-whatsapp-card/blob/main/whatsapp.html).*

## Mão na massa!


1 ) A instalação do **Tailwind** CSS é super simples e você pode conferir o tutorial oficial [clicando aqui](https://tailwindcss.com/docs/installation/framework-guides)

2 ) Os passos abaixo descrevem a instalação do **Animate CSS** em projetos Nuxt ou Vue

Para usuários **npm**, adicione animate.css em seu projeto usando este comando:

```bash
npm install animate.css --save
```

Para usuários de yarn

```bash
yarn add animate.css
````

**Importação com Nuxt JS:** no arquivo ***nuxt.config.js*** importe o CSS da seguinte forma:

```javascript
css: ['animate.css/animate.min.css']
````

**Importação com Vue JS:** Faça o import dentro do componente que iremos criar logo abaixo.

```javascript
import 'animate.css'
````

3 ) Crie um componente vue em ***components/WhatsAppCTA.vue***

4 ) Em seu componente substitua o conteúdo entre a tag **<template>...</template>** pelo código abaixo.

```html
<div class="fixed right-6 bottom-6">
    
    <transition 
      enter-active-class="animate__animated animate__fadeInRight"
      mode="out-in"
    >
      <!-- CARD TO SEND MESSAGE -->
      <div v-if="isOpen">
        <div class="w-96 max-w-[90vw] rounded-3xl overflow-hidden shadow-2xl shadow-[#075E54]/50 bg-[#E7E7E7]">
          
          <!-- Header and close button -->
          <div class="h-20 p-5 flex items-center justify-between gap-4 bg-[#25D366]">
            <div class="flex items-center gap-3">
              <img class="w-7 h-28" src="@/assets/icon/header/whatsapp.svg" alt="WP">
              <p class="text-lg font-medium text-white">WhatsApp</p>
            </div>
            <button @click="isOpen = false" class="hover:rotate-12 hover:scale-110" title="Fechar">
              <img src="@/assets/icon/close.svg" alt="Fechar" class="w-8 h-8">
            </button>
          </div>


          <!-- Message input -->
          <div class="p-4 py-6">
            <input type="text" name="message" id="message" v-model="form.message" maxlength="140" title="Mensagem"
              class="w-full px-4 py-4 rounded-full text-sm border-none text-[#075E54]">
          </div>


          <!-- Send button -->
          <div class="w-full p-4 flex justify-end">
            <button @click="goToWhatsAppChat" id="send-whatsapp-message" title="Enviar mensagem"
              class="px-5 py-2 rounded-full flex items-center justify-between gap-1 bg-[#25D366] hover:scale-105 hover:shadow-lg hover:shadow-[#075E54]/30 transition-all duration-300">
              <p class="font-medium text-white">Abrir Conversa</p>
              <img src="@/assets/icon/send.svg" alt="Enviar">
            </button>
          </div>


        </div>
      </div>


      <!-- BUTTON TO OPEN SEND MESSAGE CARD -->
      <button v-else @click="openWhatsAppCard" id="open-whatsapp-card" 
        class="w-16 h-16 rounded-full grid place-content-center hover:scale-105 transition-all duration-300 bg-[#25D366] shadow-xl shadow-[#075E54]/20" title="WhatsApp">
        <img src="@/assets/icon/header/whatsapp.svg" alt="WhatsApp" class="w-8 h-8">
      </button>
    </transition>


  </div>
```

5 ) Ainda no componente substitua a tag **<script>...</script>** pelo conteúdo abaixo

```javascript
<script lang="ts">
import Vue from 'vue';


export default Vue.extend({
  data() {
    return {
      isOpen: false,
      form: {
        message: "Falar com nossa equipe agora!",
        number: '5562988887777'
      }
    }
  },
  methods: {
    openWhatsAppCard() {
      this.form.message = "Falar com nossa equipe agora!"
      this.isOpen = true
      // ... Dispare qualquer outra coisa aqui
    },
    goToWhatsAppChat() {
      this.isOpen = false;
      let message = (this.form.message === "Falar com nossa equipe agora!")? " " : this.form.message;
      window.open(`https://api.whatsapp.com/send?phone=${this.form.number}&text=${message}`, '_blank')
      this.form.message = "Falar com nossa equipe agora!"
      // ... Dispare qualquer outra coisa aqui
    }
  }
});
</script>
````
> **Caso não esteja utilizando TypeScript em seu projeto, remova `lang="ts"` no inicio da tag `<script>`**.
    
6 ) No objeto form dentro da função **`data( )`**, substitua os valores das propriedades conforme necessário.

7 ) No método `openWhatsAppCard( )` substitua o valor da propriedade `this.form.message` pelo mesmo utilizado no objeto form da função `data( )`, faça o mesmo no método `goToWhatsAppChat( )`

8 ) Para utilizar o componente com Nuxt basta fazer sua declaração na(s) página(s) ou no layout, com Vue puro faça a importação no App.vue.

**Sim, isso é tudo! Seu componente de integração com o WhatsApp está pronto para uso.**

[**Vou deixar aqui o código completo**](https://github.com/Karytonn/nuxtjs-whatsapp-card/blob/main/WhatsAppCTA.vue) e você pode simplesmente copiar e colar fazendo as devidas adequações.

Quer ver uma demostração, [**esse é o site de um cliente real**](https://www.procopioeoliveira.com.br/) onde implementamos esta funcionalidade.

---

Se isso te ajudou de alguma forma, não deixe de curtir e compartilhar esse artigo 😉

---
ah... qualquer coisa conte comigo!
[LinkedIn](https://www.linkedin.com/in/karytonn/)
[GitHub](https://github.com/Karytonn)
[Instagram](https://www.instagram.com/karytonn.dev/)
[Twitter](https://twitter.com/karytonn)
[www.karytonn.dev](https://karytonn.dev)