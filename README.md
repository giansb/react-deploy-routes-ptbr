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
  "homepage": "https://{nome do usuario}.github.io/{nome do repositorio}/"
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


## Enviando projeto para um repositório

Caso não tenha o repositório criado, vamos fazer isso agora, para isso siga os passos:

<div style="display: inline">
  <img src="https://github.com/giansb/react-deploy-routes-ptbr/assets/107221898/2d1e844f-84c6-4077-96cb-d507eb13af5f"/>
  <img src="https://github.com/giansb/react-deploy-routes-ptbr/assets/107221898/7862db0e-4abc-47ae-9e42-e4c817486c10"/>
</div>

Agora vamos escolher um nome para o repositório, evitando colocar espaço, se necessário, substituir por '-'. Logo depois é só clicar em "Create repository".

<img src="https://github.com/giansb/react-deploy-routes-ptbr/assets/107221898/8ec042ad-69c2-4d0c-9549-705ca9ba3f65"/>

<p>O Github vai gerar um link, de direcionamento para o repositório:</p>
<img src="https://github.com/giansb/react-deploy-routes-ptbr/assets/107221898/d7c2c128-eb67-4646-a44e-a092eb3ec3f8"/>

<p>ATENÇÃO: relembrando que é necessário declarar o nome do repositório no package.json:</p>

 ```diff
{
  "name": "starter-project",
  "homepage": "https://{nome do usuario}.github.io/{nome do repositorio}/"
  "version": "0.1.0",
  ...
}
````

##

<p>Agora vamos voltar para o nosso projeto. Dentro do terminal, vamos iniciar o git com o seguinte comando:</p>
<strong>git init</strong>

<p>Vamos adicionar todos os arquivos que está dentro da pasta:</p>
<strong>git add .</strong>

<p>Damos um nome para o nosso commit</p>
<strong>git commit -m "primeiro-commit"</strong>

<p>Nessa parte vamos dizer qual o caminho do repositório do github. Para isso vamos usar o link gerado no próprio:</p>
<strong>git remote add origin "https://github.com/{usuario}/{repositorio}.git"</strong>

<p>Agora vamos usar o push para mandar todos os nossos arquivos para lá:</p>
<strong>git push -u origin main</strong>








