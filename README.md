# 🛡️ Ansible Astra Hardening

Ansible-плейбук для автоматической настройки безопасности **Astra Linux Common Edition** после установки.  
Это инфраструктурный код (IaC), который заменяет ручной скрипт `astra-hardening` и даёт преимущества декларативного подхода.

---

## 📦 Что делает плейбук

- Обновляет систему (`apt update && apt upgrade`)
- Устанавливает и настраивает файрвол **ufw** (разрешён только SSH)
- Отключает ненужные службы (cups, bluetooth, avahi-daemon)
- Настраивает политику паролей (минимальная длина 12 символов, сложность)
- Включает автоматические обновления безопасности (`unattended-upgrades`)
- Включает системный аудит (`auditd`)
- Настраивает SSH (запрет root-входа с паролем, отключение парольной аутентификации)

---

## 🚀 Запуск

### 1. Установка Ansible

Если Ansible ещё не установлен:

```bash
sudo apt update
sudo apt install ansible -y
```

### 2. Клонирование репозитория

```bash
git clone https://github.com/IlyaTrihkin/ansible-astra-hardening.git
cd ansible-astra-hardening
```

### 3. Запуск плейбука

```bash
ansible-playbook playbook.yml
```

---

## ⚙️ Настройка

Плейбук использует локальное подключение (`connection: local`).
Чтобы применить его к удалённым серверам, измени `hosts` и добавь `ansible_user` / `ansible_ssh_private_key_file`.

---

## 🧪 Проверка результата

```bash
ufw status
systemctl status ssh
ssh localhost   # должен зайти по ключу без пароля
```

---

## 📁 Структура проекта

```text
ansible-astra-hardening/
├── playbook.yml        # Основной плейбук
├── README.md
└── LICENSE
```

---

## 📌 Примечания

- Плейбук разработан для Astra Linux Common Edition 2.12.

- Для работы по SSH требуется предварительно настроенный ключ.

- Службы, отсутствующие в системе (например, bluetooth), игнорируют

---

## 👤 Автор

Илья Тришкин — специалист по информационной безопасности.

#### GitHub: 
https://github.com/IlyaTrihkin

#### TenChat: 
https://tenchat.ru/ilya_trishkin

#### Habr: 
https://habr.com/ru/users/ilya_trishkin

---

## 📄 Лицензия

Этот проект распространяется под лицензией MIT. Подробнее см. [LICENSE](LICENSE).
