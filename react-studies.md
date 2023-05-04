# Curso React: Instalando o React (create-react-app) - #02

- node.js
- `npx create-react-app my-app-name` 
- build: transforma o app estatico
- executar: `npm start`

- dir node_modules: dependencias (criado com `npm install`)
- dir public: 
- src: js, css, fonte etc
    - App.js is main


# Curso React: Entendendo o JSX - #03

- JSX: html in js
- variavel: declara dentro de 
```js
function App(){

    const name = 'eu'
    const newName = name.toUpperCase()
    const url = 'https://via.placeholder.com/150'

    function sum(a, b){
        return a + b
    }

    return (
        <div className="App">
            <p>{name}</p>
            <p>soma: {2 + 2}</p>
            <p>soma: {sum(1, 2)}</p>
            <img src={url} alt="imagem" />
        </div>
    )
}
```
- todos os elementos devem estar wrapped em div ou className
    - `class` eh palavra reservada de react


# Curso React: Criando componentes no React - #04

- dividir a aplicação em partes
- criar arquivos `.js` e exportar; importar para usar
- normalmente ficam na pasta `components`

- dentro da pasta `src/components/`
- componente iniciando com Maiuscula e camelcase
- HelloWorld.js
```js
// geralmente com mesmo nome do arquivo
// declarar function == declarar que eh um component
function HelloWorld(){
    return (
        <div>
            <h1>Meu primeiro componente</h1>
        </div>
    )
}

export default HelloWorld
// mesmo nome do arquivo para export
// precisa para exportar o componente
```

- em App.js
```js
import HelloWorld from './components/HelloWorld'

// code

    return (
        <div className="App">
            <HelloWorld />
        </div>
    )

```


# Curso React: Trabalhando com props - #05

- `props`: valores passados para componentes (comp. filho recebe uma propriedade do comp. pai)
- o valor é passado como um atributo na chamada do componente

- componente filho
```js
function SayMyName(props){
    return (
        <div>
            <p>Fala ai {props.nome}, suave?</p>
        </div>
    )
}

export default SayMyName
```

- componente pai
```js
import SayMyName from './components/SayMyName';

function App() {
    const nome = 'Judy'
    return (
        <div className="App">
            <SayMyName nome="Caio"/>
            <SayMyName nome={nome}/>
        </div>
    );
}

export default App;
```

- para evitar repeticao da palavra props podemos refatorar de
```js
function Pessoa(props){
    return (
        <div>
            <img src={props.foto} alt={props.nome} />
            <p>nome: {props.nome}</p>
            <p>idade: {props.idade}</p>
            <p>profissao: {props.profissao}</p>
        </div>
    )
}

export default Pessoa
```
- para
```js
function Pessoa({ nome, idade, profissao, foto }){
    return (
        <div>
            <img src={foto} alt={nome} />
            <p>nome: {nome}</p>
            <p>idade: {idade}</p>
            <p>profissao: {profissao}</p>
        </div>
    )
}

export default Pessoa
```


# Curso de React: Inserindo CSS no React (CSS modules) - #06

- css pode ser adicionado de forma global, por meio de arquivo `index.css`
- a nivel componentes `NomeDoComponente.module.css` e chamar ela no componente
- nao pode ter classes com traço (-)
    - react entende como subtracao
    - usar apenas underline e camelCase (`.fraseContainer` ou `.frase_container`)

- arquivo main
```js
import styles from 'dir/to/arquivo'
// code
function Frase(){
    return (
        <div className={styles.fraseContainer}>
            <p className={styles.fraseContent}>este eh a frase a ter css aplicada</p>
        </div>
    )
}
export default Frase
```



# Curso React: Utilizando React fragments - #07

- criação de um componente sem elemento pai
    - nao precisa de div (?)
- sintaxe: <> e </> (tag vazia)
- criamos no proprio jsx
- se precisar de div, criar componente
    - esse fragment eh so um fragment, tipo uma linha do codigo

- fragment:
```js
function List(){
    return (
        <>
            <h1>Minha lista</h1>
            <ul>
                <li>item 1</li>
                <li>item 2</li>
            </ul>
        </>
    )
}

export default List
```
- outro fragment exemplo:
```js
function Item(props){
    return (
        <>
            <li>{props.marca}</li>
            <p>go to homepage</p>
        </>
        // cria varios items li segundo o q esta no props.marca
    )
}
export default Item
```

- na main:
```js
import List from 'dir/to/file'
// codigo

    <List />
```



# Curso React: Avançando em props - #08

- definir tipos para props, realizando uma especie de validacao
- definimos em um objeto chamado propTypes no proprio componente
- pode definir um valor padrao

```js
import PropTypes from 'prop-types'

function Item({ marca, ano_lancamento }){

    return (
        <>
            <li>
                {marca} - {ano_lancamento}
            </li>
        </>
    )

}

// propTypes minuscula pq eh a propriedade do componente
Item.propTypes = {
    marca: PropTypes.string,
    ano_lancamento: PropTypes.number,
}

// valor default
// tipo qnd para esperar carregar os dados do BD ou qnd o cliente nao preenche o valor, entao deixa NA como default
Item.defaultProps = {
    marca: 'Faltou a marca',
    ano_lancamento: 0,
}

export default Item
```



# Curso React: Eventos no React (onClick, onChange e onSubmit) - #09

- eventos para responder a um click
- o evento é atrelado a uma tag que irá executá-lo
- geralmente um método é atribuído ao evento

- evento se coloca dentro da tag (geralmente método), mas sem () pq vira invocação de método

- chamar <Evento numero="4"/> na App.js principal
```js
function Evento({ numero }){

    function meuEvento(){
        console.log(`Activated! ${numero}`)
    }

    return(
        <div>
            <p>Clique aqui para disparar um evento</p>
            <button onClick={meuEvento}>Ativar!</button>
        </div>
    )
}

export default Evento
```

- forms
```js
function Form(){

    function cadastrarUsuario(e){
        e.preventDefault() 
        // para o envio de dado (submit) para back e executa a funcao
        // e == evento, interceptar o valor
        console.log("Usuario cadastrado")
    }

    return (
        <div>
            <h1>Meu cadastro</h1>
            <form onSubmit={cadastrarUsuario}>
                <div>
                    <input type="text" placeholder="Digite o seu nome" />
                </div>
                <div>
                    <input type="submit" value="Cadastrar" />
                </div>
            </form>
        </div>
    )
}

export default Form
```



# Curso React: useState na prática - #10

- manusear o estado de um componente
- ex) salvar os valores enviados pelo form antes de enviar pra back
- `import { useState } from 'react'`

-
```js
import { useState } from 'react'

function Form(){

    function cadastrarUsuario(e){
        e.preventDefault() 
        console.log(name)
        console.log("Usuario cadastrado")
    }

    const [password, setPassword] = useState()
    const [name, setName] = useState('Valor Default')
    // setName para atribuir o valor
    // name = para resetar o valor 
    // duas constantes setName para valor q a gnt quer trabalhar outro name para alterar ??????????

    return (
        <div>
            <h1>Meu cadastro</h1>
            <form onSubmit={cadastrarUsuario}>
                <div>
                    <label htmlFor="name">Nome :</label>
                    <input 
                        type="text" 
                        id="name" 
                        name="name" 
                        placeholder="Digite o seu nome" 
                        value={name}
                        onChange={(e) => setName(e.target.value)}
                    />
                </div>
                <div>
                    <label htmlFor="password">Senha :</label>
                    <input 
                        type="password" 
                        id="password" 
                        name="password" 
                        placeholder="Digite a sua senha" 
                        onChange={(e) => setPassword(e.target.value)}
                    />
                </div>
                <div>
                    <input type="submit" value="Cadastrar" />
                </div>
            </form>
        </div>
    )
}

export default Form
```


# Curso React: Passar eventos por props - #11

- pode criar pasta dentro de components

-
```js
// no metodo q chama o button
// meuEvento tem q estar declarado
// pai
<Button event={meuEvento} text="Primeiro Evento" />

// filho
function Button (props){
    return <button onClick={props.event}>{props.text}</button>
}
```

# Curso React: Renderização condicional (if) - #12

- envolvemos as tags em chaves {}
- as chaves executam js
- eh possivel usar o `state` para criar as condicoes

-
```js
import { useState } from 'react'

function Conidicional(){

    const [email, setEmail] = useState()
    const [userEmail, setUserEmail] = useState()

    function limparEmail(e){
        e.preventDefault()
        setUserEmail('') // define como false
    }

    function enviarEmail(e){
        e.preventDefault()
        setUserEmail(email)
    }

    return (
        <div>
            <h2>Cadastre o seu email</h2>
            <form>
                <input 
                    type="email" 
                    placeholder='Digite seu email' 
                    onChange={(e) => setEmail(e.target.value)}
                />
                <button type="submit" onClick={enviarEmail}>Enviar email</button>
                {/* {userEmail} pra impprimir userEmail se existir */}
                {userEmail && ( // se existir userEmail, faz isso
                    <div>
                        <p>O email do usuario eh {userEmail}</p>
                        <button onClick={limparEmail}>Limpar email</button>
                    </div>
                )}
            </form>
        </div>
    )
}

export default Conidicional
```


# Curso React: Renderização de listas - #13

- array (geralmente eh array de objetos) -> funcao map para percorrer

- 
```js
function OutraLista({ itens }){

    return (
        <>
            <h3>Lista de coisas</h3>
            {
                // jsx
                itens.map((item) => (
                    <p>{item}</p>
                    // se for objeto {item.nome}
                ))
                // acho q equivale a for item in itens
            }
        </>
    )
}

export default OutraLista
```

- Warning: Each child in a list should have a unique key prop
```js
itens.map((item, index) => (
    <p key={index}>{item}</p>
))
```
- eh pra o react tem id de referencia, no front nn muda nada. nao eh bom usar index, geralmente eh id q vem do back 

- se lista for vazia?
```js
<h3>Lista de coisas</h3>
{ itens.length > 0 ? ( // if ternario
    itens.map((item, index) => (
        <p key={index}>{item}</p>
    ))) : ( // else
        <p>Nao ha itens na lista!</p>
    )
}
```


# Curso React: State Lift - #14

- pra compartilhar o state
- elevar o nivel do estado a um componente pai
- centralizar o state no pai e definir quem usa e quem define (setState)

- 
```js
function SeuNome({ setNome }){

    //const [nome, setNome] = useState()
    // not using this anymore!

    return (
        <div>
            <p>Digite seu nome:</p>
            <input 
                type="text" 
                placeholder="Qual eh o seu nome?"
                onChange={(e) => setNome(e.target.value)}
            />
        </div>

    )

}

export default SeuNome
```

-
```js
function Saudacao({ nome }){

    function gerarSaudacao(algumNome){
        return `Ola, ${algumNome}, td bem?`
    }

    // imprime o nome so se tiver
    return (
        <>
            {nome && <p>{gerarSaudacao(nome)}</p>}
        </>
    )

}

export default Saudacao
```

- main
```js
function App() {

  const [nome, setNome] = useState()

  return (
    <div className="App">
      <h1>State Lift</h1>
      <SeuNome setNome={setNome} />
      {nome}
      <Saudacao nome={nome} />
    </div>
  )
}
```



# Curso React: Implementando o React Router - #15

- `npm install react-router-dom`
-
```js
import { BrowserRouter as Router, Switch, Route, Link } from 'react-router-dom'

function App() {

  return (
    <Router>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/empresa">Empresa</Link>
        </li>
        <li>
          <Link to="/contato">Contato</Link>
        </li>
      </ul>
    </Router>
  )
}

export default App
```
- em `/src/pages` criar Home.js Contato.js etc (sempre cria como se fosse componente)