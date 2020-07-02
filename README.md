# React 

## Terminal
Para criar o app:

```
npx create-react-app my-app-name
cd my-app-name
npm start
```
Vai abrir o navegador com o endereço: http://localhost:3000/


## Atom (ou IDE de escolha)

Abrir pasta do projeto.
No index.js existe a função:
```
ReactDOM.render(
    <App />,
  document.getElementById('root')
);
```
que vai renderizar o componente <App /> no seu index.html

#### Componentes
O react é desenvolvido de forma que os componentes que a gente crie sejam reutilizáveis:
Para criar um componente, crie um novo arquivo Componente.js
```
import React from 'react'

function Componente(){

  return(
    <div>
        conteúdo do componente
    </div>
  )
}
export default Componente
```
e pode ser acrescentado dentro de outro componente, assim:

```
import React from 'react';

import Componente from './Componente'

function App() {
  return (
    <div>
      <Componente />
    </div>
  );
}

export default App;
```


## Se for usar Material-Ui
```
npm install @material-ui/core
```
#### Se quiser usar ícones:
```
npm install @material-ui/icons
```
Material ui foi desenvolvido baseado na fonto Roboto, para instalar acrescentar no index.html:
```
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" 
```

#### USO:
```
import React from 'react'
import { Button } from '@material-ui/core';

function MyButton(){
  return(
    <Button variant="outlined" color="primary" href="#send">
      ENVIAR
    </Button>
  ) 
}
export default MyButton
```

#### Customizar CSS com material-ui
```
import { makeStyles } from '@material-ui/core'

const useStyles = makeStyles(theme => ({
  container: {
    background: 'rgb(230, 230, 230)',
    display: 'flex',
    flexFlow: 'row nowrap',
    justifyContent: 'space-around',
    alignItems: 'stretch',
    minHeight: '100vh',
    padding: 15,
  },
  postSpace:{
    marginBottom: 15,
  },
}))

function Componente(){
  const classes = useStyles()

  return(
    <div className={classes.container}>
    </div>
```



## Deploy

- Acessar firebase.com ; criar o projeto
```
firebase init

```
npm run build
firebase deploy
```
