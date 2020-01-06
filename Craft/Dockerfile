FROM balenalib/raspberry-pi-debian:buster
MAINTAINER Athit Kao (github.com/atet)
RUN printf "deb-src http://raspbian.raspberrypi.org/raspbian/ buster main contrib non-free rpi" >> \
   /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y apt-utils 
RUN apt-get install -y python-pip cmake libglew-dev xorg-dev libcurl4-openssl-dev doxygen git
RUN apt-get -y build-dep glfw
RUN python -m pip install requests
RUN git clone https://github.com/fogleman/Craft.git /usr/local/Craft
WORKDIR "/usr/local/Craft/"
RUN cmake -Wno-dev .
RUN make
RUN gcc -std=c99 -O3 -fPIC -shared -o world -I src -I \
   deps/noise \
   deps/noise/noise.c \
   src/world.c
RUN cp server.py server.py.BAK && \
   sed "s/AUTH_REQUIRED = True/AUTH_REQUIRED = False/" server.py.BAK > \
   server.py
EXPOSE 4080
CMD ["python", "./server.py"]
