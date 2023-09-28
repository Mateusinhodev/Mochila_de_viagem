# Mochila_de_viagem
Projeto desenvolvido juntamente com a Alura no curso: JavaScript na Web - armazenando dados no navegador 

### Manipulando dado no navegador

- **Capturando os dados da tela**
    
    ```jsx
    const form = (document.getElementById("novoItem"));
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        console.log(evento.target.elements['nome'].value)
        console.log(evento.target.elements['quantidade'].value)
    
    })
    ```
    

> O método `preventDefault()` cancela o evento se for cancelável, o que significa que a ação padrão que pertence ao evento não ocorrerá. ~ W3School
> 

Nessa primeira etapa do projeto, criamos uma variável com o nome `form` e com ela capturamos e armazenamos o elemento do HTML identificado com um id `novoItem` com o método do DOM `getElementById`.

Com a variável criada, passamos a ela o `addEventListener` contendo como evento o `submit` (enviar formulário) e também criamos uma função anônima que tem como parâmetro o `“evento”` e nele serão armazenado os dados do formulário, a partir dele adicionaremos o `preventDefault` que irá interromper o envio de dados para a página e irar enviar o dados para o navegador. Por fim, iremos percorrer os elementos para mostrar no `console` (ferramenta do desenvolvedor) através do `console.log` o dados nome e quantidade inserido pelo usuário.

- **Criando as validações**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        criaElemento(evento.target.elements['nome'].value, evento.target.elements['quantidade'].value);
    });
    
    function criaElemento(nome, quantidade) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = quantidade;
    
        novoItem.appendChild(numeroItem);
        novoItem.innerHTML += nome;
    
        lista.appendChild(novoItem);
    }
    ```
    

> O `appendChild()`método anexa um nó (elemento) como o último filho de um elemento.
> 

Começamos essa etapa, com a criação de um novo elemento, para isso criamos uma variável chamada `novoItem`, essa variável armazena a criação de um novo item `li` que foi feito por meio do `document.createElement` e também adicionamos uma `class` `“item”` ao novo elemento por meio do `classList.add`.

Seguindo em frente, criamos outra variável chamada `numeroItem`, ela mostrará a quantidade de determinado acessório inserido pelo usuário. Para isso, foi realizado o mesmo comando anterior de criação de um novo elemento por meio do `document.createElement`. E para inserirmos o valor que foi inserido pelo usuário dentro da `tag strong`, devemos utilizar o `innerHTML`, juntamente com a variável que está armazenando o elemento do `HTML` e passar a eles a `quantidade` (parâmetro que recebe o valor dos acessórios).

Agora precisamos adicionar o valor armazenado dentro da variável `numeroItem`, dentro do elemento que foi criado e armazenado dentro da variável `novoItem`, dessa seguinte forma:

```html
<li class="item"><strong>7</strong>Camisas</li>
```

Se observamos o código acima, temos um `strong`, dentro de uma `li`, e é isso que fizemos no JavaScript utilizando o `appendChild` e logo depois passamos um `innerHTML` na variável `novoItem` e passamos a ele o parâmetro `nome`.

E para finalizarmos, criamos outra variável que seleciona e armazena o elemento do `HTML` que está identificado com um `id` chamado `“lista”` e dentro da função `criaElemento`, chamamo-o e com o `appendChild` adicionamos tudo que está armazenado dentro da variável `novoItem` e assim fizemos com que os dados que foi inserido pelo usuário, fique visível na tela. 

### Armazenando dados na Web

- **O armazenamento na WEB**

> O **`localStorage`** faz parte de uma API JavaScript chamada Web Storage. Sendo uma ótima ferramenta para armazenar pares de **chave | valor** no computador do usuário.
> 
- **Inserindo dados no LocalStorage**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        criaElemento(nome.value, quantidade.value);
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(nome, quantidade) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = quantidade;
    
        novoItem.appendChild(numeroItem);
        novoItem.innerHTML += nome;
    
        lista.appendChild(novoItem);
    
        localStorage.setItem("nome", nome);
        localStorage.setItem("quantidade", quantidade);
    
    }
    ```
    

Pra iniciarmos, mudamos algumas coisas para deixarmos o código mais limpo, então dentro do `addEventListener`, criamos duas variáveis chamada `“nome”` e `“quantidade”` e dentro delas adicionamos seus elementos e se executarmos o código, veremos que para adicionar outro item, é necessário que apague o valor inserido anteriormente, isso significa que o valor está ficando salvo e precisamos zera-lo, para isso, passaremos a variável que criamos acompanhado de `value` e passaremos uma `string` vazia `“”`.

Partindo para o armazenamento na web, utilizamos dentro da função `criaElemento` o `localStorage.setItem` e nele passamos o valor nome e quantidade enviados pelo o usuário. Porém quando executados, observamos que quando adicionamos dois novos itens, apenas um será salvo no navegador, pois eles estão se sobrescrevendo um ao outro.

- **Múltiplos itens no LocalStorage**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    itens = []
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        criaElemento(nome.value, quantidade.value);
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(nome, quantidade) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = quantidade;
    
        novoItem.appendChild(numeroItem);
        novoItem.innerHTML += nome;
    
        lista.appendChild(novoItem);
    
        const itemAtual = {
            "nome": nome,
            "quantidade": quantidade
        }
    
        itens.push(itemAtual)
    
        localStorage.setItem("item", JSON.stringify(itens));
    
    }
    ```
    

Como vimos anteriormente, quando criávamos múltiplos itens, eles acabavam se sobrescrevendo, para isso criamos um `objeto` chamado `itemAtual` e nele passamos os valores adicionados pelo usuário, depois passamos esse objeto, para o `localStorage`, porém precisamos converter a forma dos valores que estavam em `objeto` para `string` já que o `localStorage` do navegador não ler objeto, apenas string e para resolver esse problema, utilizamos `JSON.stringify`.

Mas ainda não terminamos, como os objeto ainda estavam sobrescrevendo uns aos outros, então criamos um `array` com nome `“itens”`, e dentro dele colocamos o objeto `itemAtual`, e passamos ele para o `localStorage`.

### Interagindo com dados da web

- **Consultando dados do LocalStorage**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        console.log(elemento.nome, elemento.quantidade);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        criaElemento(nome.value, quantidade.value);
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(nome, quantidade) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = quantidade;
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += nome;
    
        lista.appendChild(novoItem);
    
        const itemAtual = {
            "nome": nome,
            "quantidade": quantidade
        }
    
        itens.push(itemAtual)
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
    }
    ```
    

> O método `getItem()` retorna o valor do item do objeto de armazenamento especificado.
> 

> O método `forEach()` executará uma função para cada elemento presente em um array.
> 

Na etapa anterior, temos uma variável que armazena um array vazio, e esse array vazio é quem armazena os dados adicionados pelo usuário e o salva no `localStorage`. Porém se executarmos o código, veremos que precisamos ainda buscar os dados que estão armazenados.

Para isso, usamos o `getItem` dentro da variável `“itens”`, ou seja, será verificado se já existe dados salvos no `localSotage`, caso não há, será adicionado a nova informação no array vazio que vem logo em seguida, por isso o uso do operador `ou (||)`.

Logo após, abrimos um `forEach` acompanhado da variável `itens` e de uma função anônima, o `foreach` ira passear pelo array, pegando todos os seus dados, e como foi passado, irá executar a impressão dos dados. Porém descobrimos um problema, e precisamos de passar o `JSON.parse`, para transforma-lo de `string` como fizemos com `JSON.stringfy` para `objeto` e resolver o problema. E assim, fizemos a busca dos dados salvos no `localStorage`.

- **Atualizar página ao cadastrar item**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        criaElemento(elemento);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        const itemAtual = {
            "nome": nome.value,
            "quantidade": quantidade.value
        }
    
        criaElemento(itemAtual);
    
        itens.push(itemAtual)
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(item) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = item.quantidade;
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += item.nome;
    
        lista.appendChild(novoItem);
    }
    ```
    

> Nós refatoramos o nosso código para que a responsabilidade da função criar elemento seja única e exclusiva para criar o elemento, nós refatoramos o nosso *submit*, o enviar do formulário para que ele agora gerencie todas as funções que precisam ser gerenciadas neste momento do envio do item e nossa página é carregada buscando os dados no Local Storage, iterando em cima deles e criando cada um dos elementos.
> 

### Atualizando um item

- **Modificar a quantidade de um item**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        criaElemento(elemento);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        const existe = itens.find( elemento => elemento.nome === nome.value);
    
        const itemAtual = {
            "nome": nome.value,
            "quantidade": quantidade.value
        }
    
        if (existe) {
            itemAtual.id = existe.id;
            console.log(existe.id);
    
            atualizaElemento (itemAtual);
        } else{
            itemAtual.id = itens.length;
    
            criaElemento(itemAtual);
            
            itens.push(itemAtual);
        }
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(item) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = item.quantidade;
        numeroItem.dataset.id = item.id
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += item.nome;
    
        lista.appendChild(novoItem);
    
    }
    
    function atualizaElemento (item) {
        document.querySelector("[data-id='" + item.id +"']").innerHTML = item.quantidade;
    }
    ```
    

Nessa etapa de atualização, criamos uma variável chamada `existe`, e adicionamos a ela juntamente ao `array itens` o método `find`, ele fará com que, quando um novo item for adicionado o `find` irá verificar no `array` `itens` se já existe algum valor `idêntico (===)` ao que está sendo adicionado.

Seguindo o código temos uma condição `if e else`, que representa o seguinte: Se existe for verdadeiro (true), simplificando, se existe algum `item` idêntico ao novo `item` que ta sendo adicionado, será executado a nova função `atualizaElemento`. Se não existe será executado a função `criaElemento`.

Para identificarmos cada item, o melhor a se fazer é direcionar um `id` para ele, esse id é um número e podemos dizer que é um código, e será seu identificador, assim como usamos o id lá no `HTML`. Para inserirmos esse `id/código`, faremos o mesmo passo a passo que fizemos para adicionar a tag `strong`, e então cada item terá o seu id, de forma que ajudará na atualização dos itens.

E por fim, explicando a nova função `atualizaElemento`, ele selecionará o item a depender de seu id e através do `innerHTML`, atualizará sua `quantidade`.

Porém se atualizarmos a página, perderemos a atualização do item, para resolvermos esse problema, precisamos ainda atualizar os itens la no `localStorage`.

- **Atualizando um item do LocalStorage**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        criaElemento(elemento);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        const existe = itens.find( elemento => elemento.nome === nome.value);
    
        const itemAtual = {
            "nome": nome.value,
            "quantidade": quantidade.value
        }
    
        if (existe) {
            itemAtual.id = existe.id;
            console.log(existe.id);
    
            atualizaElemento (itemAtual);
    
            itens[existe.id] = itemAtual
        } else{
            itemAtual.id = itens.length;
    
            criaElemento(itemAtual);
            
            itens.push(itemAtual);
        }
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(item) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = item.quantidade;
        numeroItem.dataset.id = item.id
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += item.nome;
    
        lista.appendChild(novoItem);
    
    }
    
    function atualizaElemento (item) {
        document.querySelector("[data-id='" + item.id +"']").innerHTML = item.quantidade;
    }
    ```
    

Aqui o passo a passo foi bem simples, para fazer com que os itens sejam atualizados, adicionamos apenas uma linha de código no `if`, que significa que, se existe um item idêntico ao novo item que está sendo adicionado, esse novo item irá sobrescreve-lo no `localStorage`.

### Removendo um item

- **Removendo um item da mochila**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        criaElemento(elemento);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        const existe = itens.find( elemento => elemento.nome === nome.value);
    
        const itemAtual = {
            "nome": nome.value,
            "quantidade": quantidade.value
        }
    
        if (existe) {
            itemAtual.id = existe.id;
            console.log(existe.id);
    
            atualizaElemento (itemAtual);
    
            itens[itens.findIndex(elemento => elemento.id === existe.id)] = itemAtual
        } else{
            itemAtual.id = itens[itens.length - 1] ? (itens[itens.length - 1]).id + 1 : 0;
    
            criaElemento(itemAtual);
            
            itens.push(itemAtual);
        }
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(item) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = item.quantidade;
        numeroItem.dataset.id = item.id
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += item.nome;
    
        novoItem.appendChild(botaoDeleta(item.id))
    
        lista.appendChild(novoItem);
    
    }
    
    function atualizaElemento (item) {
        document.querySelector("[data-id='" + item.id +"']").innerHTML = item.quantidade;
    }
    
    function botaoDeleta(id) {
        const elementoBotao = document.createElement("button");
        elementoBotao.innerText = "X";
    
        elementoBotao.addEventListener("click", function () {
           deletaElemento(this.parentNode, id);
        })
    
        return elementoBotao;
    }
    
    function deletaElemento(tag, id) {
        tag.remove();
    
        itens.splice(itens.findIndex( elemento => elemento.id === id), 1)
    
        localStorage.setItem("itens", JSON.stringify(itens))
    }
    ```
    

Quase finalizando o projeto, chegamos na parte de excluir elemento e para isso, criamos uma nova função com o nome `botaoDeleta`, dentro dessa função, criamos um elemento do tipo `button` com o
comando `createElement` e o armazenamos dentro da variável `elementoBotao`.

Seguindo, criamos um evento de `click`, que quando o elemento `button` for clicado, irá executar a função `deletaElemento`, nessa nova função, utilizamos como parametro  `tag`, no caso a `tag button`, e passamos a ela um `remove`, para excluirmos, porém quando o código for executado perceberemos que quando clicamos no botão `"X"`, excluiremos o elemento botão e não o item da mochila. Para resolvermos, passamos um `parentNode` no `deletaElemento`, para pegar todas as
tags parentes, ou seja, pegará todas as tags que estão inclusas uma dentro da outra.

- **Removendo um item do LocalStorage**
    
    ```jsx
    const form = document.getElementById("novoItem");
    const lista = document.getElementById('lista');
    const itens = JSON.parse(localStorage.getItem("itens")) || [];
    
    console.log(itens);
    console.log([]);
    
    itens.forEach( (elemento) => {
        criaElemento(elemento);
    })
    
    form.addEventListener("submit", (evento) => {
        evento.preventDefault();
    
        const nome = evento.target.elements['nome'];
        const quantidade = evento.target.elements['quantidade'];
    
        const existe = itens.find( elemento => elemento.nome === nome.value);
    
        const itemAtual = {
            "nome": nome.value,
            "quantidade": quantidade.value
        }
    
        if (existe) {
            itemAtual.id = existe.id;
            console.log(existe.id);
    
            atualizaElemento (itemAtual);
    
            itens[itens.findIndex(elemento => elemento.id === existe.id)] = itemAtual
        } else{
            itemAtual.id = itens[itens.length - 1] ? (itens[itens.length - 1]).id + 1 : 0;
    
            criaElemento(itemAtual);
            
            itens.push(itemAtual);
        }
    
        localStorage.setItem("itens", JSON.stringify(itens));
    
        nome.value = "";
        quantidade.value = "";
    });
    
    function criaElemento(item) {
        const novoItem = document.createElement('li');
        novoItem.classList.add("item");
    
        const numeroItem = document.createElement('strong');
        numeroItem.innerHTML = item.quantidade;
        numeroItem.dataset.id = item.id
        novoItem.appendChild(numeroItem);
    
        novoItem.innerHTML += item.nome;
    
        novoItem.appendChild(botaoDeleta(item.id))
    
        lista.appendChild(novoItem);
    
    }
    
    function atualizaElemento (item) {
        document.querySelector("[data-id='" + item.id +"']").innerHTML = item.quantidade;
    }
    
    function botaoDeleta(id) {
        const elementoBotao = document.createElement("button");
        elementoBotao.innerText = "X";
    
        elementoBotao.addEventListener("click", function () {
           deletaElemento(this.parentNode, id);
        })
    
        return elementoBotao;
    }
    
    function deletaElemento(tag, id) {
        tag.remove();
    
        itens.splice(itens.findIndex( elemento => elemento.id === id), 1)
    
        localStorage.setItem("itens", JSON.stringify(itens))
    }
    ```
    

Finalizando o projeto, a gente já concluiu a etapa de excluir o itens da mochila, mas nessa ultima missão temos que excluir o item do `localStorage`. E para isso dentro da função `deletaElemento`, iremos pegar o `array` que contém a lista de itens presente na mochila e que estão gravados no `localStorage`, passar um `splice` e manipular o código para executarmos essa remoção.

Com o `splice` a gente precisará afirmar a ele a posição do elemento que queremos excluir, (e é aqui que está o pulo do gato), não poderemos passar uma posição qualquer, pois o nosso projeto não está programado, para que seja dessa forma.

Então precisamos implementar o `id` nessa função, e com isso, acontecerá uma “bagunça” nas atribuições dos `id` para cada elemento. 

E para resolvermos essa “bagunça”, é necessário voltarmos lá na condição `if else`, onde começamos a manipulação da implementação dos `id`. E fazer com que no último elemento do `array itens`, encontrado através do `length`, e adicionamos +1 ao `id` desse ultimo elemento, porém existe a possibilidade, desse `array` estar vazio, então precisamos, pensar em uma lógica, para resolvermos esse possivel problema. 

> Eu vou fazer aqui um *if*, *if else*, só que eu vou usar o operador ternário. O operador ternário eu simplesmente faço uma interrogação, se positivo faça a primeira condição, se negativo faça a outra. Se o meu *array* não existe, se não tem nada, o Id que eu quero dar para o elemento é o Id 0, essa é a minha condição final. Se não existir nada no *array* o Id vira 0, agora se já tiver alguma coisa no Id eu quero achar no último elemento o Id e aí sim, eu quero adicionar 1 a ele.
>
