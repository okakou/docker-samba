# Base image
FROM debian:stretch

# Maintainer
MAINTAINER Kouta Okamoto <okakou0512@gmail.com>

# Set non interactive install
ENV DEBIAN_FRONTEND=noninteractive

# Install samba
RUN apt-get update && apt-get install -y samba

# charset
RUN sed -i '/\[global\]/a\   unix charset = UTF-8'          /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   display charset = UTF-8'       /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   dos charset = CP932'           /etc/samba/smb.conf
# network 
RUN sed -i '/\[global\]/a\   interfaces = 127.0.0.0/8 eth0' /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   bind interfaces only = yes'    /etc/samba/smb.conf
# access to symlink
RUN sed -i '/\[global\]/a\   wide links = yes'              /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   unix extensions = no'          /etc/samba/smb.conf
# disable printer
RUN sed -i '/\[global\]/a\   load printers = no'            /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   printing = bsd'                /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   printcap name = /dev/null'     /etc/samba/smb.conf
RUN sed -i '/\[global\]/a\   disable spoolss = yes'         /etc/samba/smb.conf
# access directory
RUN sed -i '$a[share]'                                      /etc/samba/smb.conf
RUN sed -i '$a\   path           = /home/share'             /etc/samba/smb.conf
RUN sed -i '$a\   writable       = no'                      /etc/samba/smb.conf
RUN sed -i '$a\   guest ok       = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\   guest only     = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\   create mode    = 0777'                    /etc/samba/smb.conf
RUN sed -i '$a\   directory mode = 0777'                    /etc/samba/smb.conf
RUN sed -i '$a\   share modes    = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\\'                                           /etc/samba/smb.conf
RUN sed -i '$a[upload]'                                     /etc/samba/smb.conf
RUN sed -i '$a\   path           = /home/upload'            /etc/samba/smb.conf
RUN sed -i '$a\   writable       = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\   guest ok       = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\   guest only     = yes'                     /etc/samba/smb.conf
RUN sed -i '$a\   create mode    = 0777'                    /etc/samba/smb.conf
RUN sed -i '$a\   directory mode = 0777'                    /etc/samba/smb.conf
RUN sed -i '$a\   share modes    = yes'                     /etc/samba/smb.conf

RUN mkdir -p /home/share
RUN ln -s /home/master                                      /home/share/master

RUN mkdir -p /home/upload
RUN ln -s /home/master                                      /home/upload/master

# port settings
EXPOSE 139
EXPOSE 445

# Set run command
CMD [ "bash", "-c", "nmbd -D && smbd -F </dev/null" ]
