# HyperV-VMs-Ansible-Role

Ansible роль для автоматического создания машин на локальном hyper-V с Cloud Init

## Что нужно для запуска?

- Удаленный хост с Windows, на котором установлен SSH Server и включен Hyper-V

- Локальный хост с установленным Ansible:
	- Windows с WSL 
	- Unix подобная система  

## Как запустить?

Первое, что нужно сделать - скачать cloud image. В моем случае я скачивал Ubuntu Server: [тык](https://cloud-images.ubuntu.com/noble/current/) 
Формат - .img

Далее нужно установить qemu именно на unix подобные системы. В моем случае была WSL:
```bash
sudo apt update && sudo apt upgrade
sudo apt install -y qemu-utils
```

Далее конвертируем файл, который скачали ранее:
```shell
qemu-img convert -f qcow2 -O vhdx focal-server-cloudimg-amd64.img focal-server-cloudimg-amd64.vhdx
```
Данный файл требуется перенести любым удобным способом на удаленный хост Windows.

Перед запуском следует экспортировать публичный ключ:
```bash
export SSH_KEY="$(cat ~/.ssh/<ключ>)"
```

## Известные проблемы
1. Cloud Init не отрабатывает для конфигурации сети
2. Возможно неэффективное использование джоб в Ansible
3. Возможны лишние джобы
4. Не все переменные динамически создаются

В любом случае все это в ближайшее время будет дорабатываться 