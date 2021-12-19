<template>


<a-form-model layout="inline" :model="formInline" @submit="handleSubmit" @submit.native.prevent>
  <h1>ACCESO</h1>

  <a-form-model-item>
    <a-input v-model="formInline.user" placeholder="USUARIO">
    <a-icon slot="prefix" type="user" style="color:rgba(0,0,0,.25)" />
    </a-input>
  </a-form-model-item>

  <a-form-model-item>
    <a-input v-model="formInline.password" type="password" placeholder="CONTRASEÑA">
    <a-icon slot="prefix" type="lock" style="color:rgba(0,0,0,.25)" />
    </a-input>
  </a-form-model-item>

  <a-form-model-item>
    <a-button type="primary" html-type="submit" :disabled="formInline.user === '' || formInline.password === ''">
    <NuxtLink to="/logged"> Ingresar </NuxtLink>
    </a-button>
  </a-form-model-item>
</a-form-model>


</template>
<script>
export default {
    layout: 'login',
  data() {
    return {
      formInline: {
        user: '',
        password: '',
      },
    };
  },
  methods: {
    handleSubmit(e) {
      console.log(this.formInline);
    },
  },
};
</script>
