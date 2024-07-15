<template>
  <q-page padding>
    <q-form
      @submit="onSubmit"
      class="row q-gutter-sm"
    >
      <q-input
        outlined
        v-model="form.title"
        label="Título"
        lazy-rules
        class="col-lg-6 col-x-12"
        :rules="[ val => val && val.length > 0 || 'Campo Obrigatório']"
      />
      <q-input
        outlined
        v-model="form.author"
        label="Autor"
        lazy-rules
        class="col-lg-6 col-x-12"
        :rules="[ val => val && val.length > 0 || 'Campo Obrigatório']"
      />

      <div class="col-lg6 col-xs-12" >
        <q-editor v-model="form.content" min-height="5rem" />
      </div>
      
      <div class="col-12 q-gutter-sm" >
        <q-btn label="Salvar" color="white" text-color="primary" class="float-right" icon="save" type="submit"/>
        <q-btn label="Cancelar" color="red" class="float-right" icon="save" :to="{name: 'home'}"/>
      </div>
    </q-form>
  </q-page>
</template>

<script>

import { defineComponent, onMounted, ref } from 'vue';
import postsService from 'src/services/posts';
import { useQuasar } from 'quasar';
import { useRouter, useRoute } from 'vue-router';


export default defineComponent({
  name: "FormPost",
  setup() {
    const { post, getById, update } = postsService();
    const $q = useQuasar()
    const router = useRouter()
    const route = useRoute()
    const form = ref({
      title: '',
      content: '',
      author: ''
    });

    onMounted( async () => {
      if(route.params.id){
        const response = await getById(route.params.id)
        console.log(response)
        form.value = response
      }
    })

    const onSubmit = async () => {
      console.log("Form submitted", form);
      try {
        if (form.value.id) {
          await update(form.value)
        } else {
          await post(form.value)
        }
        $q.notify({message: "Post salvo com sucesso!", icon:"check", color:"positive"})
        router.push({name: "home"})
        // form.value = { title: '', content: '', author: '' };
        console.log("Post enviado com sucesso!");
      } catch (error) {
        console.log("Erro ao enviar o post:",error)
      }
      
    };

    return {
      form,
      onSubmit,
  
    };
  }
});
</script>