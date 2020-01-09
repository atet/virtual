FROM balenalib/raspberry-pi-debian:buster
MAINTAINER Athit Kao (github.com/atet)
RUN printf "deb-src http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi" >> \
   /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y apt-utils git
RUN apt-get install -y python-pip build-essential
RUN python -m pip install requests
RUN git clone https://github.com/atet/Craft.git /usr/local/Craft
WORKDIR "/usr/local/Craft/"
RUN gcc -std=c99 -O3 -fPIC -shared -o world -I src -I \
   deps/noise \
   deps/noise/noise.c \
   src/world.c
EXPOSE 4080
CMD ["python", "./server.py"]