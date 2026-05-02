# Tailscale

Este repositório contém a configuração necessária para implantar o Tailscale usando Docker e Docker Compose. O container está configurado com a rede em modo *host* e para funcionar, por padrão, como um *exit node*.

## Pré-requisitos

* Docker instalado
* Docker Compose instalado
* Uma conta no [Tailscale](https://tailscale.com/)

## Como implantar

Siga os passos abaixo para configurar e iniciar o Tailscale:

1. **Acesse a pasta do projeto:**

   Após clonar o repositório, acesse a pasta raiz:
   ```bash
   cd tailscale
   ```

2. **Crie o arquivo de ambiente (`.env`):**

   O arquivo `.env_example` está disponível no repositório.
   ```bash
   cp .env_example .env
   ```
   
   Edite o arquivo `.env` para definir o nome do container e o hostname do dispositivo na sua rede Tailscale. Altere a variável `TAILSCALE_NAME`:
   ```env
   TAILSCALE_NAME=docker-rasp
   ```

3. **Inicie o serviço:**

   Execute o Docker Compose para iniciar o container:
   ```bash
   docker compose up -d
   ```

4. **Autentique o dispositivo na rede (Tailnet):**

   Como não há uma chave de autenticação pré-configurada, você precisará gerar e acessar a URL de login através dos logs do container.

   Verifique os logs executando:
   ```bash
   docker logs docker-rasp
   ```

   Nos logs, procure por uma mensagem semelhante a esta:
   `To authenticate, visit: https://login.tailscale.com/a/xxxxxxxxxxxx`

   Copie o link, abra no seu navegador e faça o login para aprovar a inclusão deste node na sua rede.

5. **Aprovar rotas e Exit Node (Opcional):**
   
   O container está configurado para anunciar a si mesmo como um *exit node*. Para efetivar essa configuração:
   
   1. Acesse o **Admin Console** do Tailscale no navegador.
   2. Vá na aba **Machines**.
   3. Encontre o seu novo dispositivo (`docker-rasp`).
   4. Habilite a opção **"Use as exit node"** para permitir que outros dispositivos da rede usem a internet através deste container.

