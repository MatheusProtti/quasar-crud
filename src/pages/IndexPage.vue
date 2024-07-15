<template>
  <q-page padding>
    <q-table title="Artigos" :rows="posts" :columns="columns" row-key="id" 
    >

    <template v-slot:top>
      <span class="text-h4">Bibilioteca</span>
      <q-space/>
      <q-btn color="primary" label="Novo" :to="{name: 'formPost'}" />
    </template>
     <template v-slot:body-cell-actions="props">
      <q-td :props="props" class="q-gutter-sm">
        <q-btn icon="delete" color="negative" dense size="sm" @click="deletePost(props.row.id)" />
        <q-btn icon="edit" color="info" dense size="sm" @click="editPost(props.row.id)" />
      </q-td>
     </template>
    </q-table>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from "vue";
import postsService from 'src/services/posts'
import { useQuasar } from 'quasar'
import { QEditor } from 'quasar';
import { useRouter } from "vue-router";

const posts = ref([]);
const { list, remove } = postsService()
const columns = [
  { name: "id",
    field: "id",
    label: "Id",
    sortable: true,
    align: "left", 
  },
  {
    name: "title",
    field: "title",
    label: "Titulo",
    sortable: true,
    align: "left",
  },
  {
    name: "author",
    field: "author",
    label: "Autor",
    sortable: true,
    align: "left",
  },
  {
    name: "actions",
    field: "actions",
    label: "Ações",
    align: "right",
  },
];

const $q = useQuasar()
const router = useRouter()

const getPosts = async () => {
  try {
    const data = await list()
    console.log("Posts recebidos:", data); // Verifique os dados recebidos
    posts.value = data
    console.log("Posts recebidos:", data);
  } catch (error) {
    console.error("Erro ao buscar os posts:", error);
  }
};

const deletePost = async (id) => {
  console.log("Tentando deletar o post com id:", id);
  try {
    console.log("id:",id)
    $q.dialog({
        title: 'Deletar',
        message: 'Deseja deletar este post ?',
        cancel: true,
        persistent: true
      }).onOk(async() => {
        console.log("id:",id)
         await remove(id);
         $q.notify({message: "Apagado com sucesso!", icon:"check", color:"positive"})
         await getPosts();
      })
  } catch (error) {
    $q.notify({message: "Apagado com sucesso!", icon:"times", color:"negative"})
  }
};

const editPost = (id) => {
  router.push({ name: 'formPost', params: {id} })
}

onMounted(() => {
  getPosts();
});

defineOptions({
  name: "IndexPage",
});
</script>
