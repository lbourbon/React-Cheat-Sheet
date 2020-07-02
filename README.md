# React Cheat Sheet

## Terminal

Para criar o app:
```
npx create-react-app my-app-name
cd my-app-name
npm start
```
Vai abrir o navegador com o endereço: http://localhost:3000/

Se for usar router (Route, Link, Redirect...)
```npm install react-router-dom```

Se for usar Material-UI: 
```npm install @material-ui/core```


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

##### Componentes
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

#### Routes

```
import {BrowserRouter as Router} from 'react-router-dom'
ReactDOM.render(
      <Router>
          <App />
      </Router>,
    document.getElementById('root')
```

```
import {Switch, Route} from 'react-router-dom'

function App() {
  return (
    <div>
        <Nav />
        <Switch>
            <Route exact path="/"><Home /></Route>
            <Route exact path="/home"><Home /></Route>
            <Route exact path="/login"><Login /></Route>
            <Route exact path="/aprenda" component={Aprenda} />
            <PrivateRoute exact path="/aprenda/:curso" component={Curso} />
        </Switch>
    </div>
  )
}
export default App;
```
##### Link
```
import {Link} from 'react-router-dom'

<Link to="/home" className={classes.item}>HOME</Link>
```


##### useParams  - usar parâmetros da url
```
import {useParams} from 'react-router'
const {param1, param2} = useParams()
```
##### useHistory
```
import {useHistory} from 'react-router'
const history = useHistory()
history.goBack()
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
    <Button variant="outlined" color="primary" onClick={() => { alert('clicked') }}>
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

## HOOKS

useState :  para qualquer dado mutável dinamicamente:
```
import { useState } from 'react';

const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>+</button>
```
useEfect : para operar efeitos colaterais, mudar algo quando uma variável mudar, no exemplo abaixo quando count muda, a função executa e re-renderiza o valor
se usar [ ] o array vazio, a função executa quanto o componente monta
se acrescentar um return antes da } , passar uma função no return que executa quando o componente desmonta
```
useEffect(() => {
  document.title = `Você clicou ${count} vezes.`
}, [count])
```



## Context 

```
import React, { useState, useEffect } from 'react'
import firebase from 'firebase/app'
import "firebase/auth";

const UserContext = React.createContext()

function UserContextProvider(props){

  const [isSignedIn, setIsSignedIn] = useState(false)
  const [currentUser, setCurrentUser] = useState("")

  useEffect(() => {
    firebase.auth().onAuthStateChanged(
      (user) => {
        setIsSignedIn(!!user)
        setCurrentUser(user)
      }
    )
  }, [])

  function signOut() {
    firebase.auth().signOut()
  }

  return <UserContext.Provider value={{isSignedIn, signOut, currentUser}}>
            {props.children}
         </UserContext.Provider>
}

export  {UserContextProvider, UserContext}
```

NO INDEX.js
```
import {UserContextProvider} from './context/userContext'

ReactDOM.render(
    <UserContextProvider>
      <Router>
          <App />
      </Router>
    </UserContextProvider>,
    document.getElementById('root')
)
```

USANDO:
```
import React, {useContext} from 'react'
const { isSignedIn, currentUser } = useContext(UserContext)
```


## Deploy

- Acessar firebase.com ; criar o projeto
```
firebase init

```
npm run build
firebase deploy
```
