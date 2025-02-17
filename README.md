# Front Chatbot-IA

<center>

![Logo ChatbotIA](https://raw.githubusercontent.com/Almeedus/Chatbot-IA/refs/heads/main/src/Logo.png)

</center>

> Imagem de autoria própria


<hr>

## 🌐 Visão Geral
O Front Chatbot IA é uma interface construída em VueJS que permite que os usuários utilizem o sistema por meio de requesições contendo dúvidas baseadas nos editais de vestibular do Instituto Federal de São Paulo.

<hr>

## 🗃️ Índice
- [Chatbot-IA](#chatbot-ia)
  - [🌐 Visão Geral](#-visão-geral)
  - [🗃️ Índice](#️-índice)
  - [💻 Pré-Requisitos](#-pré-requisitos)
  - [🛠️ Stack Utilizada](#️-stack-utilizada)
    - [Stack de Instalação do Windows](#stack-de-instalação-do-windows)
    - [Stack de Instalação do Linux](#stack-de-instalação-do-linux)
  - [🚩 Iniciando a Aplicação](#-iniciando-a-aplicação)
    - [⬇️ Clonando o Repositório](#️-clonando-o-repositório)
    - [⚙️ Instalando dependencias](#️-instalando-dependencias)
  - [⚓ Endpoints](#-endpoints)
    - [📒 Editais](#-editais)
<hr>

## 💻 Pré-Requisitos
- Node; 
- VueJS 3.2.13 instalado;


OBS.: Caso o sistema operacional usado seja o Windows é necessário instalar e ativar o WSL para a instação do Redis

[`📗 Guia de Instação Node`](https://nodejs.org/pt)
[`📙 Guia de Instação VueJS`](https://www.npmjs.com/package/vue/v/3.2.13)

<hr>

## 🛠️ Stack Utilizada
A linguagem ecolhida foi o VueJS com o TypeScript pela sua facilidade na construção de interfaces de Single-Applications, comunidade ativa e por limitações de hardware do desenvolvedor. 

### Stack de Instalação do Windows
![Diagrama da Stack](https://raw.githubusercontent.com/Almeedus/Chatbot-IA/refs/heads/main/src/diagrama-stack-windows.png)

### Stack de Instalação do Linux
![Diagrama da Stack](https://raw.githubusercontent.com/Almeedus/Chatbot-IA/refs/heads/main/src/diagrama-stack-linux.png)
> Imagem feita utilizando o [Canva](https://www.canva.com/)

<hr>

## 🚩 Iniciando a Aplicação
Antes de tudo você deve ter o Node e o VueJS instalados conforme os [pré-requisitos](#-pré-requisitos).

> [!NOTE]
> Sem a instalação dessas tecnologias a aplicação não irá rodar.

### ⬇️ Clonando o Repositório
Use o comando `git clone` para clonar este repositório ou faça o [download](https://github.com/Almeedus/ChatbotIA-Front/archive/refs/heads/main.zip) do mesmo:
```bash
git clone https://github.com/Almeedus/ChatbotIA-Front.git
```

### ⚙️ Instalando dependencias 
É importante instalar as dependencias do sistema antes de iniciar a aplicação:
```bash
npm install
```

Compila e recarrega automaticamente para desenvolvimento
```
npm run serve
```

Compila e minimiza para produção
```
npm run build
```

Verifica e corrige arquivos
```
npm run lint
```

<hr>

## ⚓ Endpoints

### 📒 Editais
| EndPoint | Método | Descrição | Corpo da Requisição |
| --- | --- | --- | --- |
| / | GET | Teste | N/A |
| /duvidas | POST| Inserir uma pergunta | `{"query": "Informe sua pergunta"}` |
