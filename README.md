# Enviando Mensagens de WhatsApp com a API do Facebook

## Introdução

Neste projeto, desenvolvemos um código em Python que utiliza a API do Facebook Graph para enviar mensagens do WhatsApp. O código permite enviar mensagens de um número padrão fornecido pela API do WhatsApp diretamente para o seu número de telefone. Este guia irá detalhar o funcionamento do código, bem como fornecer exemplos visuais (prints) de cada etapa do processo.

## Preparação do Ambiente

Primeiro, certifique-se de ter as bibliotecas necessárias instaladas e as variáveis de ambiente configuradas. Utilizamos a biblioteca `dotenv` para carregar as variáveis de ambiente, que incluem o token de acesso (`ACCESS_TOKEN`), o ID do número de telefone (`PHONE_NUMBER_ID`), e o número do destinatário (`RECIPIENT_WAID`).

## .env

```
ACCESS_TOKEN=""

APP_ID=""
APP_SECRET=""
RECIPIENT_WAID="" # Seu número de whatsapp com o código do seu pais e região
VERSION="v18.0"
PHONE_NUMBER_ID=""

VERIFY_TOKEN=""
```

## Carregando Variáveis de Ambiente

```python
import json
import requests
from dotenv import load_dotenv
import os

load_dotenv()
ACCESS_TOKEN = os.getenv("ACCESS_TOKEN")
APP_ID = os.getenv("APP_ID")
APP_SECRET = os.getenv("APP_SECRET")
RECIPIENT_WAID = os.getenv("RECIPIENT_WAID")
VERSION = os.getenv("VERSION")
PHONE_NUMBER_ID = os.getenv("PHONE_NUMBER_ID")
VERIFY_TOKEN = os.getenv("VERIFY_TOKEN")
```

## Função para Enviar Mensagem de Texto
### A função send_message é responsável por configurar a solicitação HTTP e enviar a mensagem de texto para o número especificado.

```python 
def send_message(text):
    url = f"https://graph.facebook.com/{VERSION}/{PHONE_NUMBER_ID}/messages"
    header = {"Authorization": "Bearer " + ACCESS_TOKEN,
              "Content-type": "application/json"}

    data = {
        "messaging_product": "whatsapp",
        "recipient_type": "individual",
        "to": RECIPIENT_WAID,
        "type": "text",
        "text": {"preview_url": False, "body": text}
    }
    response = requests.post(url, headers=header, json=data)

if __name__ == "__main__":
    send_message(input("qual msg vc gostria de se enviar?"))
```

# Explicação do Código
## URL da API:

A URL é construída utilizando as variáveis de ambiente, especificando a versão da API e o ID do número de telefone.

### Cabeçalhos:

Incluem o token de acesso para autenticação e indicam que o conteúdo da solicitação está em formato JSON.

### Dados da Mensagem:

O campo data contém os detalhes da mensagem, incluindo o produto de mensagens (WhatsApp), o tipo de destinatário (individual), o número do destinatário, o tipo de mensagem (texto) e o corpo da mensagem.

### Envio da Solicitação:

A solicitação POST é enviada para a URL da API com os cabeçalhos e os dados especificados. A resposta da solicitação é verificada para confirmar se a mensagem foi enviada com sucesso.

## Prints do Processo
### 1. Configurando as Variáveis de Ambiente

### 2. Construindo a URL e os Cabeçalhos

### 3. Estrutura dos Dados da Mensagem

### 4. Enviando a Mensagem

### 5. Resposta da API

# Conclusão
Este código permite enviar mensagens de texto utilizando a API do WhatsApp de maneira eficiente e segura. Através da configuração adequada das variáveis de ambiente e do uso correto da API do Facebook Graph, podemos automatizar o envio de mensagens para qualquer número de telefone. 

