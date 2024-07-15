# Projeto Final (projetofinal)

Projeto Final Do Semestre, utilizando quasar framwork, Vue 3, axios e json-serverfoi criado um CRUD.

Utilizando o axios para consumir uma api no front-end criamos um projeto novo para servir como a nossa Base de Dados e instalamos o json-server.

## Instale as dependências
```bash
npm install json-server
```

## Crie a estrutura base:
```bash
{
  "posts": [
    {
      "id": "1",
      "title": "Senhor dos Anéis",
      "author": "J.R.R. Tolkien",
      "content": "Livro: J.R.R. Tolkien"
    }
  ]
}
```
npx json-server db.json
## Inicie o banco
```bash
npx json-server db.json
```
Agora o Projeto 

## Instale as dependências
```bash
yarn
# or
npm install
```

### Inicie o aplicativo no modo de desenvolvimento (recarregamento de código ativo, relatório de erros, etc.)
```bash
quasar dev
```


### Lint os arquivos
```bash
yarn lint
# or
npm run lint
```


### Formate os arquivos
```bash
yarn format
# or
npm run format
```



### Crie o aplicativo para produção
```bash
quasar build
```

### Clonar o Projeto
```bash
https://github.com/MatheusProtti/quasar-crud.git
```

### Personalize a configuração
See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).
