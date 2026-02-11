FROM alpine:3.19

# Установка базовых пакетов
RUN apk add --no-cache \
    openssh-server \
    python3 \
    py3-pip \
    sudo

# Генерация SSH‑ключей (критически важно!)
RUN ssh-keygen -A

# Настройка SSH
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    echo 'root:alpine123' | chpasswd

# Создание пользователя ansible
RUN adduser -D -s /bin/sh ansible && \
    echo 'ansible:ansible' | chpasswd && \
    adduser ansible wheel

# Создание необходимых директорий
RUN mkdir -p /var/run/sshd

# Проверка корректности конфигурации SSH перед запуском
RUN sshd -t

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
