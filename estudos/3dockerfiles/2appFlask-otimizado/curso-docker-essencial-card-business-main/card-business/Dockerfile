# para otimizar um contêiner, você tem três opções:
# 1) Usar uma imagem base mais leve e que consuma menos recursos
# 2) Fazer menos instalações ou usar tecnologias mais leves (em recursos e tamanho)
# 3) Usar o cache do Docker ao seu favor


# o cache do Docker funciona da seguinte maneira:
# toda vez que você roda uma imagem, ele cria um cache dela
# logo, se você recriar a mesma imagem de novo, ele a criará mais rápido
# contudo, ele descarta o cache a partir da primeira camada que tiver alterações
# no seu Dockerfile. Por isso, para usar o cache da forma mais eficiente,
# as camadas que possuem mais alterações a cada criação de imagem
# devem ficar por último no seu Dockerfile, pois assim você consegue
# usar o cache nas primeiras camadas e criar a imagem mais rápido


# usarei o python como imagem base, pois aí já terei a ferramenta e seu ecossistema
# ao invés de ter que baixar um Ubuntu inteiro, o que é desnecessário
# e usarei a imagem oficial do Python com a TAG do Alpine, pois ele é um sistema leve
# então o Python estará rodando num sistema operacional simples, leve e performático
FROM python:3.9-alpine

EXPOSE 8000

WORKDIR /app

COPY requirements.txt .

RUN pip3 install --no-cache-dir -r requirements.txt

ENV LOGOMARCA="../public/linkedin.png"
ENV FOTO="../public/fotoPerfil.png"
ENV NOME="I-Juca-Pirama"
ENV IDADE="30"
ENV EMAIL="juca@gmail.com"
ENV PROFISSAO="Escritor"
ENV SITE="www.linkedin.com"

COPY . .

CMD [ "python3", "app.py" ]