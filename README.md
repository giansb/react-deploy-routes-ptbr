# React.js: Github-pages com Router

<p>Esse artigo-tutorial vai ser um guia básico de como configurar as rotas da sua página web para fazer deploy com o Github Pages. No fim deste documento vai estar o link de duas referências que me ajudaram a desenvolver ele.</p>

<p><p/>


## Instalando o gh-pages

<p>Com o seu projeto React aberto, execute o seguinte comando no terminal:</p>
<strong>npm install gh-pages –save-dev</strong>
<p>- Ele irá instalar os pacotes necessários para preparar o package.json para o deploy.</p>

## Configurando o package.json

<p>Vamos abrir o nosso arquivo package.json e adicionar a seguinte propriedade no topo:</p>
  
 ```diff
{
  "name": "starter-project",
  "homepage": "https://tomerpacific.github.io/{nome do repositorio}/"
  "version": "0.1.0",
  ...
}
````

<p>Atenção: não esqueça de substituir a última parte pelo nome do seu repositório</p>

<p>Em seguida, vamos adicionar mais duas propriedades em “scripts”:</p>

````diff
"scripts": {
    "start": "react-scripts start",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build", 
    "build": "react-scripts build",
    "test": "react-scripts test",
    ...
  },
````
<p>feito isso, seu package.json já está pronto para o deploy</p>

## Rotas da página

<p>Essa parte foi a que me fez começar a escrever esse artigo. Primeiro vamos instalar a biblioteca do react router, para isso rodamos o seguinte comando no terminal:</p>
<strong>npm install react-router-dom</strong>

<p>e vamos organizar as rotas da seguinte maneira: </p>


<strong>index.js</strong>
````diff

import { HashRouter } from 'react-router-dom';


const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <HashRouter>
      <App />
    </HashRouter>
  </React.StrictMode>
);


````
<strong></strong>
<strong>App.js</strong>
````diff
import {Routes, Route } from 'react-router-dom';


function App() {
  return (
    <div className="App">
      <Routes>
          <Route exact path="/" element={<PagHome/>}></Route>
          <Route path="/projetos" element={<PagProjetos/>}></Route>
      </Routes>
    </div>
  );
}

````
##

<p>Agora para usar as rotas criadas, ao invés de usar a tag <a href=><a/>, vamos instalar mais um pacote, chamado react-router-hash-link. Instalamos com o seguinte comando:</p>
<strong>npm install react-router-hash-link</strong>
<p>No meu caso, irei usar as rotas no componente que cabeçalho:</p>

````diff

  import { HashLink } from 'react-router-hash-link';


export default function Topo(){
    return(
        <header>
            <div className='topo limita-secao'>
                <div class="button" tabindex="0">
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </div>
                <p>Gian  S Braga | <span className='azul'>Dev</span> Front-end</p>
                    <nav>
                        <HashLink to="/">Inicio</HashLink>
                        <HashLink to="/#curriculo" smooth>Currículo</HashLink>
                        <HashLink to="/projetos#top" smooth>Projetos</HashLink>
                        <HashLink to="/#contato" smooth>Contato</HashLink>
                    </nav>
               
            </div>
        </header>
    );
}
````
<p>a propriedade smooth permite que ao entrar na pagina, ele usa o scrool suavemente até a seção com o id indicado, não é obrigatória declarar. Assim como o texto “#top”, ele vem como definição para mandar para o topo da página indicada. Para mais comandos a parte, acesse a documentação do HashLink.</p>
<p>Agora com a nossa página já funcionando, chegou a vez de mandar para o repositório, aqui vai um tutorial bem básico de como fazer isso:</p>




