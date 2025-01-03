# isso é um comentário


# este comando serve para você dizer qual será a imagem base do projeto
# você pode adicionar a TAG :latest para alocar versões, mas isso não é recomendável
# pois caso haja alguma alteração numa versão futura, o projeto pode parar de funcionar
FROM ubuntu:22.04


# este comando serve para executar comandos na imagem que você chamou em FROM
# este && \ serve para não precisar de dois RUN para executar esses comandos
# e ele é necessário, porque pacotes de atualização expiram após serem executados
# então é necessário fazer no mesmo comando para que não expirem antes
RUN apt-get update && \
    apt-get install -y \
    python3.11 \
    python3.11-dev \
    python3-pip \
    build-essential \
    libssl-dev \
    libffi-dev \
    python3-venv \
    && apt-get clean


# faz verificações para verificar se tudo foi instalado corretamente (apenas para depuração)
RUN python3 --version && pip3 --version


# altera o diretório atual, igual o comando CD do Windows/Linux
# se o diretório não existir, como é o caso aqui, ele cria o diretório
WORKDIR /app


# este comando copia todo o diretório e subdiretórios de um local A para um local B
# o primeiro ponto indica o diretório onde o comando de build do Dockerfile é realizado
# não importa onde está seu arquivo Docker, fazendo o build, o Docker encontra o Dockerfile
# e cria a imagem. Contudo, o Docker só copiará arquivos para colar em outro lugar
# a partir de onde você fez o build da imagem. Por isso, recomenda-se fazer o build
# no local onde está o Dockerfile para garantir que o comando COPY sempre copie tudo.
# O segundo ponto indica onde você colará os arquivos. Se você colocar um ponto como fiz,
# significa que ele colará tudo no diretório atual, que no caso, é o /app
# você não precisa colocar pontos nos parâmetros. Pode simplesmente colocar o endereço
COPY . .


RUN pip3 install --no-cache-dir -r requirements.txt


# este comando expõe a porta que a aplicação utiliza
# mais tarde, esta porta deve ser mapeada com a porta do host durante a criação do contêiner
EXPOSE 8000


# este comando define o que será executado toda vez que contêiners gerados por essa imagem
# forem executados. Observação: esse comando só é executado na inicialização do contêiner.
# Ele não é executado durante a criação da imagem. Aliás, existem outras formas de fazer
# esse comando, mas a forma abaixo é a mais recomendada
# neste comando, você também faz um comando shell normal, mas deve separar os argumentos
# em forma de JSON
CMD [ "python3", "app.py" ]


# para dar build na imagem, execute o comando abaixo no diretório do Dockerfile
# o ponto no final indica que você montará o build a partir do diretório atual,
# mas nada te impede de passar outro diretório
# por fim, o nome deve ser lowercase, senão não funciona
# docker image build -t <nome-imagem>:<nome-tag> .

# sugestão de como criar o container
#                           (container)                              (image name)
# docker container run --name app-py --network bridge -d -p 8080:8000 app-py:v1