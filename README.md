# 🚀 URL Shortener

URL Shortener é uma aplicação baseada em microsserviços que fornece recursos de encurtamento e redirecionamento de URL. O sistema é dividido em dois projetos independentes: **CreateUrlLambda** e **RedirectUrlShortener**, ambos implementados como funções do AWS Lambda integradas ao AWS S3 para armazenamento de dados e AWS API Gateway para roteamento. 

Essa aplicação foi desenvolvida durante o curso Java da [Rocketseat](https://www.rocketseat.com.br).

---

## 🛠️ Tecnologias Utilizadas  
- **Java**: Linguagem de programação principal.  
- **AWS Lambda**: Para processamento serverless.  
- **AWS S3**: Para armazenamento das URLs encurtadas e seus metadados.  
- **AWS API Gateway**: Para expor os endpoints das APIs.  


## 🔍 Como Funciona  

### 1. Criação de URLs curtas  
- **API Gateway**: expõe a função Lambda por meio de um endpoint HTTP POST.
- Aceita uma entrada JSON contendo:
  - `originalUrl`: a URL original a ser encurtada.
  - `expirationTime`: tempo de expiração em segundos.
- Gera um código exclusivo de 8 caracteres.
- Armazena dados de URL em um bucket S3 no formato JSON.

### 2. Redirecionamento de URLs encurtadas
- **API Gateway**: expõe a função Lambda por meio de um endpoint HTTP GET.
- Lê dados do bucket S3 com base no código de URL.
- Valida se a URL expirou.
- Retorna:
  - HTTP 302 com um cabeçalho `Location` apontando para a URL original, se válida.
  - HTTP 410 se a URL expirou.
