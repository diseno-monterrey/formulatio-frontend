<template lang="pug">
  .container
    form(action="http://127.0.0.1:5000/form-example" @submit="sendForm" method="POST")
      fieldset
        label(for="nombre") nombre
        input(name="nombre" v-model="form.nombre" placeholder="waiting")
      fieldset
        label(for="posicion") posición
        input(name="posicion" v-model="form.posicion" placeholder="waiting")
      input(type="submit" value="test")
    pre {{response}}
</template>


<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'

export default {
  data() {
    return {
      form: {},
      response: ''
    }
  },
  components: {
    Logo
  },
  methods: {
    sendForm: function() {
      event.preventDefault()
      axios.post('http://127.0.0.1:5000/form-example', this.form , {
        headers: {
          'content-type': 'application/json',
        },
      }).then( response =>{
        this.response = response
      }).catch(error => {
        this.response = error
      })
    }
  }
}
</script>

<style lang="sass">
fieldset
  @apply border p-3 flex flex-col
.container
  @apply mx-auto flex flex-col
  max-width: 900px
  min-height: 100vh
  justify-content: center
  align-items: center
</style>
