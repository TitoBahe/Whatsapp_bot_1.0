Enviando Mensagens de WhatsApp com a API do Facebook

Introdução

Neste projeto, desenvolvemos um código em Python que utiliza a API do Facebook Graph para enviar mensagens do WhatsApp. O código permite enviar mensagens de um número padrão fornecido pela API do WhatsApp diretamente para o seu número de telefone. Este guia irá detalhar o funcionamento do código, bem como fornecer exemplos visuais (prints) de cada etapa do processo.

Preparação do Ambiente
Primeiro, certifique-se de ter as bibliotecas necessárias instaladas e as variáveis de ambiente configuradas. Utilizamos a biblioteca dotenv para carregar as variáveis de ambiente, que incluem o token de acesso (ACCESS_TOKEN), o ID do número de telefone (PHONE_NUMBER_ID), e o número do destinatário (RECIPIENT_WAID).

Carregando Variáveis de Ambiente

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

    

