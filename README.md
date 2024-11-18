# Aula 08-11 - App Conversão de moeda

## Avaliação

* Implemente para que o usuário possa fazer conversão de outras moedas (mínimo + 3 moedas);
* Descreva abaixo o seu entendimento acerca desta atividade, explorando as funcionalidades das classes que contruímos e os principais pontos da aplicação;

## Entrega

* Clone este repositório e faça o que se pede;
* Realize um commit das suas alterações no seu repositório;
* Envie o link do repositório na avaliação gerada no classroom;

## Descritivo do Aluno:

Pelo radiobutton da tela você seleciona as opções de conversões assim que você as seleciona você digita um valor da moeda e faz a conversão apertando o botão de conversão. Você precisa fazer uma escolha dos radiobuttons e precisa inserir um valor caso contrário ele retorna algo na tela que diz que você precisa faze-lo. 

A parte de verificação de que opções você faz é feita com um switch e verifica na API o valor da conversão para que a conta seja feita quando você apertar o botão de converter.

Para recuperar as taxas de conversão entre as moedas escolhidas (por exemplo, "Real -> Dólar", "Bitcoin -> Dólar", etc.), o código se comunica com a API. Para determinar o valor equivalente em uma moeda com base em outra, como o valor de 100 reais em dólares, essas taxas são necessárias.

## Como se comunicar com a API?

**O Método buscarDados e a Classe AwesomeClient**

A classe AwesomeClient, que parece ser uma classe personalizada feita para lidar com requisições, é utilizada para se comunicar com a API. O método buscarDados dessa classe é responsável por enviar a requisição à API, passando o código de conversão (como "BRL-USD") como argumento.

**Uso da Interface ApiCallback**

A classe AwesomeClient lida com a resposta da API utilizando um callback (a interface ApiCallback<String>). Isso significa que a requisição é enviada em segundo plano, e o código toma as providências adequadas para tratar a resposta quando ela for recebida.

**A interface ApiCallback<String> possui dois métodos:**

* onSuccess(String result): Esse método é invocado quando a resposta da API é bem-sucedida. O resultado da API—normalmente um arquivo JSON com as taxas é processado pelo código.

* onError(String error): Se ocorrer um erro na requisição (como um problema de rede ou uma falha no servidor da API), esse método é invocado.

**Respondendo à API (no onSuccess)**

Para extrair a taxa de conversão, o código precisa entender os dados quando a resposta da API chega ao método onSuccess. A biblioteca Gson é utilizada para analisar a resposta da API, que é uma estrutura de dados JSON.

Um exemplo de como o código interpreta a resposta:

* Ele verifica se a chave (por exemplo, "BRLUSD") está presente no JSON e, se estiver, a converte em um objeto da classe CurrencyRate, que é a classe que contém as informações da taxa de conversão.

* A taxa é extraída se a chave correspondente à conversão solicitada for encontrada. O código então pode exibir o resultado na interface do usuário após multiplicar o valor inserido pelo usuário pela taxa de conversão.

**Como Processar o JSON da API**

Para fazer o parsing do JSON, ou seja, converter os dados JSON em objetos Java, o código utiliza o Gson.

**Exemplo do que acontece dentro do método onSuccess:**
```bash
JsonObject jsonObject = JsonParser.parseString(result).getAsJsonObject();
```
A string result (que é a resposta da API) é convertida em um objeto JsonObject, permitindo que o código acesse facilmente as taxas específicas.

## Exemplo: 

**1 -** O usuário seleciona a opção "Real -> Dolar" no RadioButton.

**2 -** O usuário digita "100" no campo de valor. 

**3 -** O usuário pressiona o botão de conversão.

**4 -** O código realiza a requisição à API para obter a taxa de conversão de BRL para USD.

**5 -** O valor 100 é multiplicado pela taxa de conversão retornada, e o resultado é exibido.
 
