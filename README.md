# ssh_between_two_linux_servers
Инструкция как связать два линукс сервера по ssh через ssh-copy-id

Есть два линукс сервера под Ubuntu Server: vm-1 и vm-2. Нужно сделать так, чтобы под пользователем root устанавливалось ssh соединение от vm-1 на vm-2.
1. Сгенирорировать на vm-1 ssh ключ из под root:<br>
sudo -i<br>
ssh keygen
2. На vm-2 перейти под root и открыть файл конфигурации sshd:<br>
sudo -i<br>
vi /etc/ssh/sshd_config
3. В файле sshd_config найти параметры PermitRootLogin и PasswordAuthentification. Оба параметра необходимо раскомментировать и выставить им yes вместо дефолтного no и сохранить с внесенными изменениями:<br>
PermitRootLogin yes<br>
PasswordAuthentification yes
4. После сохранения изменений перезапустить демон ssh на vm-2:<br>
service sshd restart
5. Установить пароль для root на vm-2:<br>
passwd root
6. На первой машине vm-1 выполнить:<br>
ssh-copy-id root@ip-address<br>
где ip-address - это ip адрес vm-2
7. В первый раз ssh запросит root пароль от vm-2, установленный на шаге 5, ввести пароль root от vm-2
8. Все, подключение установлено. Далее вводить пароль не потребуется.
