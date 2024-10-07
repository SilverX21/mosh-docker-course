# o from é a base image, podemos ver isto no docker hub
FROM node:alpine

# o copy vai copiar da partir de um destino e vai colocar num folder destino
# "." -> vai pegar em todos os ficheiros da diretoria atual
# "/app" -> vai colocar estes ficheiros numa diretoria da imagem (esta imagem tem um file system o qual vamos criar uma diretoria chamada app)
COPY . /app

# aqui definimos a diretoria que estamos a trabalhar, assim não precisamos de definir abaixo onde estamos a trabalhar
WORKDIR /app

# aqui executamos um comando, onde temos de especificar a diretoria do local da imagem onde a app está montada (tendo em conta que estamos a usar o WORKDIR, em baixo não precisamos de definir local da pasta da imagem onde temos montado no docker - definimos isto no COPY em cima)
CMD node app.js