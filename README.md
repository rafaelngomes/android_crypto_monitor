# 💹 Android Crypto Monitor

Este é um app Android que consulta, em tempo real, a cotação do Bitcoin através da API pública do Mercado Bitcoin. Ele exibe o preço atual em reais, junto com a data e hora da última atualização dos dados.

---

# 🧱 Estrutura Geral do Projeto

Abaixo, segue uma descrição dos principais arquivos e pastas do projeto: `main`, `service`, `factory` e `model`.

## 🔸 MainActivity.kt

Responsável por:

- Exibir na tela os dados obtidos da cotação do Bitcoin.
- Configurar a interface com toolbar, botões e campos de texto.
- Fazer requisições REST assíncronas utilizando coroutines.
- Lidar com falhas de rede ou erros inesperados na resposta.

## 🔸 service/MercadoBitcoinService.kt

Interface que define o acesso ao endpoint:

- Declara o método `getTicker()` para capturar os dados de preço do BTC.
- Utiliza o Retrofit com suporte a `suspend functions`.

## 🔸 service/MercadoBitcoinServiceFactory.kt

Interface que:

- Define o método getTicker() para obter os dados de cotação da moeda BTC.
- Usa Retrofit com suporte a coroutines (via suspend fun).

## 🔸 model/TickerResponse.kt

Modelos que representam a estrutura do JSON retornado pela API:

---

# 🔄 Como o app funciona

A lógica do aplicativo segue um fluxo simples e direto para obter e exibir o valor do Bitcoin:

## 1️⃣ App é iniciado

- A `MainActivity` é carregada ao abrir o app.
- A toolbar é configurada com título e cores definidas.
- O botão de atualização (`btn_refresh`) fica pronto para receber cliques do usuário .

## 2️⃣ Usuário clica em "Refresh"

- Quando o botão "Refresh" é clicado, o método makeRestCall() é chamado.
- Essa função roda dentro de uma coroutine na `Dispatchers.Main`, permitindo a chamada à API sem travar a interface do usuário.

## 3️⃣ Requisição à API do Mercado Bitcoin

- A URL base `https://www.mercadobitcoin.net/` é usada para criar uma instância do Retrofit.
- O endpoint `/api/BTC/ticker/` é acessado pelo método `getTicker()` definido na interface MercadoBitcoinService.

## 4️⃣ Tratamento da resposta

Se a chamada for bem-sucedida:

- O valor da moeda Bitcoin (campo `last`) é transformado em `Double` e formatado como moeda brasileira.
- A data/hora (campo `date`) é convertida do timestamp UNIX para o formato `dd/MM/yyyy HH:mm:ss`.
- Os dados são exibidos nas `TextViews` correspondentes: `lbl_value` e `lbl_date`.

Se houver erro na resposta HTTP:

- Uma mensagem é exibida ao usuário via Toast, indicando o código de erro (ex: 400, 404...).

## 5️⃣ Tratamento de erros

Se houver falhas de rede, exceções ou outros problemas:

- O app exibe um alerta informando o tipo de erro ocorrido.

---

## 📸 Capturas de Tela

### Tela Inicial do Android / Tela Inicial do Aplicativo
![Image](https://github.com/user-attachments/assets/60fcc9fc-2c0b-4f97-9922-1fcd4d183fcb)




### Após clique no botão de atualização

![Image](https://github.com/user-attachments/assets/b5b9f7d6-0ebe-47bc-9f1f-a369a4ef872f)


