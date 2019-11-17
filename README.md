#/bin/bash

echo -e "\033[1;33m- - - - -> \033[01;34mScript Configurar o servidor para usar SSL/TLS Stunnel4"
echo -e "\033[1;33m #################"
echo -e "\033[1;33m- - - - -> \033[01;34mScript Configure the server to use SSL / TLS Stunnel4"
echo -e "\033[1;33m #################"
echo -e "\033[1;31mTLALOKC"
sleep 2

apt-get update -y
clear
yum update -y
apt-get install openssh-server -y
clear
apt-get install curl -y
clear
yum install openssh-server -y
clear
apt-get install openssh-client -y
clear
yum install openssh-client -y
clear
apt-get install stunnel4 -y
clear
yum install stunnel4 -y
clear
apt-get install stunnel -y
clear
yum install stunnel -y
clear

echo -e "\033[1;31m  cpturando IP"
ip=$(curl https://api.ipify.org/)
echo $ip
clear

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31minicia precionando enter"
echo -e "\033[1;33m #################"
echo -e "\033[1;31miniciando"
echo -e "\033[1;33m ######################################"
sleep 1

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31mgenerando certificado"
echo -e "\033[1;33m #################"
echo -e "\033[1;31mcertificado generado"
echo -e "\033[1;33m ######################################"
sleep 1
openssl genrsa 2048 > stunnel.key
openssl req -new -key stunnel.key -x509 -days 1000 -out stunnel.crt

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31mcreando nueva configuracion"
echo -e "\033[1;33m #################"
echo -e "\033[1;31mconfiguracion creada"
echo -e "\033[1;33m ######################################"
sleep 2
rm /etc/stunnel/stunnel.conf
clear
rm /etc/default/stunnel4
clear
cat stunnel.crt stunnel.key > stunnel.pem
mv stunnel.pem /etc/stunnel/
clear
echo -e "\033[1;31mdigite el puerto ssl que desea usar"
echo -e "\033[1;31mpuerto ssl"
read -p ": " port
clear

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31configurar stunnel.conf"
echo -e "\033[1;33m #################"
echo -e "\033[1;31mconfigurando stunnel.conf"
echo -e "\033[1;33m ######################################"
sleep 1

echo -e "\033[1;31m ###"
sleep 1
echo -e "\033[1;31m #########"
sleep 1
echo -e "\033[1;31m ################"
sleep 1
echo -e "\033[1;31m ########################"
sleep 1
echo -e "\033[1;31m ##################################"
sleep 1

echo "client = no " >> /etc/stunnel/stunnel.conf
echo "[ssh] " >> /etc/stunnel/stunnel.conf
echo "cert = /etc/stunnel/stunnel.pem " >> /etc/stunnel/stunnel.conf
echo "accept = $port " >> /etc/stunnel/stunnel.conf
echo "connect = 127.0.0.1:22" >> /etc/stunnel/stunnel.conf

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31mconfigurar stunnel4"
echo -e "\033[1;33m ###################"
echo -e "\033[1;31mconfigurado stunnel4"
echo -e "\033[1;33m ######################################"
sleep 1

echo "ENABLED=1 " >> /etc/default/stunnel4
echo "FILES="/etc/stunnel/*.conf" " >> /etc/default/stunnel4echo "OPTIONS="" " >> /etc/default/stunnel4
echo "PPP_RESTART=0" >> /etc/default/stunnel4

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31miniciando stunnel4"
echo -e "\033[1;33m ###################"
echo -e "\033[1;31miniciado stunnel4"
echo -e "\033[1;33m ######################################"
sleep 1

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31m ##### ocurriran errores estandar espere...######"
echo -e "\033[1;33m ######################################"
sleep 1
stunnel
/usr/bin/stunnel &
service ssh start 1>/dev/null 2 /dev/null
/etc/init.d/ssh start 1>/dev/null 2 /dev/null
service sshd start 1>/dev/null 2 /dev/null
/etc/init.d/sshd start 1>/dev/null 2 /dev/null
service sshd restart 1>/dev/null 2 /dev/null
/etc/init.d/sshd restart 1>/dev/null 2 /dev/null
service ssh restart 1>/dev/null 2 /dev/null
/etc/init.d/ssh restart 1>/dev/null 2 /dev/null
service stunnel4 start 1>/dev/null 2 /dev/null
/etc/init.d/stunnel4 start 1>/dev/null 2 /dev/null
service stunnel4 restart 1>/dev/null 2 /dev/null
/etc/init.d/stunnel4 restart 1>/dev/null 2 /dev/null
systemctl start stunnel4 1>/dev/null 2 /dev/null
systemctl restart stunnel 1>/dev/null 2 /dev/null
clear

echo -e "\033[1;33m ####### se produce un error normal listo###############"
sleep 2
echo -e "\033[1;33m ###########reiniciando...###########"
clear

echo -e "\033[1;33m ######################################"
echo -e "\033[1;31mconfigurado con exito iniciar prueba"
echo -e "\033[1;33m ###################"
echo -e "\033[1;31mprueba exitosa"
echo -e "\033[1;33m ######################################"
echo -e "\033[1;33m- - - - -> \033[01;34mu ip host:\033[0m $ip"
echo -e "\033[1;33m- - - - -> \033[01;34mPORT SSL:\033[0m $port
sleep 1
echo -e "\033[1;31msi no funciona reinicia con comando reboot"
sleep 2
echo -e "\033[1;33m- - ->>octavio\033[01;34mT L A L O K C"
echo -e "\033[1;33m- - ->>editado por tlalokc\033[01;34m Email tlalokc1@gmail.com"
sleep 1

