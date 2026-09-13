## Отчёт по выполнению задания (Разделы 1–6)

### Таблица артефактов и подтверждений

| Файл | Раздел | Что проверяется | Как получено / Подтверждение                                                                                                                                                   |
|---|---:|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mephi-screenshot.png` | 6 | Визуальное подтверждение | В терминале: `echo "Уникальный номер: 373182"`; скриншот получен с помощью сочетания клавиш (macOS — `Cmd+Shift+4`)                                                            |
| `history.out` | Все | Выполненные команды | `history > ~/history.out`                                                                                                                                                      |
| `stat.out` | 1, 3, 4 | Права на домашний каталог и утилиты | `stat /home/user1 > ~/stat.out`; `stat /usr/local/bin/cat_suid_demo >> ~/stat.out`; `stat /home/student/cat_cap_demo >> ~/stat.out`                                            |
| `getcap.out` | 4 | Настройка привилегий (capabilities) | `getcap /home/student/cat_cap_demo > ~/getcap.out`; (для полноты) `getcap /usr/local/bin/cat_suid_demo >> ~/getcap.out 2>&1`                                                   |
| `/etc/passwd` | 1 | Управление пользователями | Создание: `sudo useradd -u 1234 -m -s /bin/bash -G students user1`                                                                             |
| `/etc/shadow` | 1 | Управление пользователями | Пароль: `sudo passwd user1`; политика: `sudo chage -M 90 user1` и `sudo chage -l user1`                                                                                        |
| `/etc/group` | 1 | Управление группами | Группа: `sudo groupadd students`; проверка: `getent group students`; членство видно в `id user1`                                                                             |
| `/etc/sudoers` | 5 | Настройка sudo | `sudo visudo -f /etc/sudoers.d/user1-time`; проверка: `sudo -l -U user1`; проверка времени: `sudo timedatectl set-ntp false && sudo timedatectl set-time "YYYY-MM-DD HH:MM:SS"` |
| `suid-files.out` (файл с выводом поиска файлов) | 2 | Поиск SUID-файлов | `find / -xdev -type f -perm -4000 -printf '%m %u:%g %p\n' 2>/dev/null &#124; sort > "$HOME/suid-files.out"`                                                                    |
| `suid-procs.out` (файл с выводом мониторинга процессов) | 2 | Процессы c EUID=0 и RUID>=1000 | `ps -eo pid,ppid,user,ruid,euid,comm,cmd --sort=pid &#124; awk 'NR==1 ...'`                                                                                                     |
