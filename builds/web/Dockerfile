FROM	ubuntu:14.04
RUN	apt-get update -y
RUN	apt-get install apache2 -y
RUN	apt-get install apache2-utils -y
RUN	apt-get install vim -y
RUN	apt-get clean
EXPOSE	80
CMD	["apache2ctl", "-D", "FOREGROUND"]
