FROM arm32v6/alpine
MAINTAINER Athit Kao (github.com/atet)
RUN apk update
RUN apk add --update --no-cache python py-pip
RUN apk add --update --no-cache gcc musl-dev
RUN apk add --update --no-cache git
RUN python -m pip install requests
RUN git clone https://github.com/atet/Craft.git \
   /usr/local/Craft
WORKDIR "/usr/local/Craft/"
RUN gcc -std=c99 -O3 -fPIC -shared -o world -I src -I \
   deps/noise \
   deps/noise/noise.c \
   src/world.c
EXPOSE 4080
CMD ["python", "./server.py"]