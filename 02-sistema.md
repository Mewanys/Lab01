```
Linux fedora 6.19.10-300.fc44.x86_64 #1 SMP PREEMPT_DYNAMIC Wed Mar 25 18:23:49 UTC 2026 x86_64 GNU/Linux
```
`uname -a`
1) uname -a ( Команда для вывода базовой систеной информации.) В нашем случае оно показало Linux fedora 6.19.10-300.fc44.x86_64,
где 6.19.10 версия ядра Linux. 
-300 это (build) внутренний номер пакета в репозитории Fedora.
.fc44 - версия дистрибутива Fedora (44 версия).
.x86_64 - 64 битное ядро для процессоров x86.

2) Выделенная памать 4gb для удобного пользования операционной системой, ее хватит для базовых взаимодействий с системой Fedora.

3) На диск мы выделили 20gb, этого хватает для базовой системы без большого колличества пакетов. Для нашего виртуального стенда без дополнительных скачиваний было достаточно.

4) Пользователи:
root - это супер пользователь обладающий правом на выполнение всех без исключений операций: чтение, запись, изменение любых файлов, установка и удаление программ, управление другими пользователями, изменение системных настроек, запуск и остановка служб.
user - обычная учетная запись пользователя с набором своих прав, что человек может делать в системе. Вход в систему , работа со своими файлами, запуск программ , использование своих инструментов.

5) Службы:
NetworkManager - главная служба для управления сетью. Она автоматически обнаруживает сетевые подкелючения. Следит за состоянием интерфейсов и может переключать на более быстрое соединение.
Udev - диспетчер устройств. Отслеживает подключаемые устройства к пк создавая папку /dev/sdX и назначает ему права.
Systemd-resolved. Эта служба отвечает за разрешение DNS-запросов «на лету»: она следит за тем, чтобы файл /etc/resolv.conf содержал актуальные адреса серверов.
```
NAME="Fedora Linux"
VERSION="44 (Workstation Edition)"
RELEASE_TYPE=stable
ID=fedora
VERSION_ID=44
VERSION_CODENAME=""
PRETTY_NAME="Fedora Linux 44 (Workstation Edition)"
ANSI_COLOR="0;38;2;60;110;180"
LOGO=fedora-logo-icon
CPE_NAME="cpe:/o:fedoraproject:fedora:44"
DEFAULT_HOSTNAME="fedora"
HOME_URL="https://fedoraproject.org/"
DOCUMENTATION_URL="https://docs.fedoraproject.org/en-US/fedora/f44/"
SUPPORT_URL="https://ask.fedoraproject.org/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_BUGZILLA_PRODUCT="Fedora"
REDHAT_BUGZILLA_PRODUCT_VERSION=44
REDHAT_SUPPORT_PRODUCT="Fedora"
REDHAT_SUPPORT_PRODUCT_VERSION=44
SUPPORT_END=2027-05-19
VARIANT="Workstation Edition"
VARIANT_ID=workstation

11:42:42 up 7 min,  1 user,  load average: 0,23, 0,48, 0,30
```

```
Файловая система Размер Использовано  Дост Использовано% Cмонтировано в
/dev/nvme0n1p3      18G         3,7G   15G           21% /
devtmpfs            16G            0   16G            0% /dev
tmpfs               16G          92K   16G            1% /dev/shm
tmpfs              6,3G         5,0M  6,3G            1% /run
none               1,0M            0  1,0M            0% /run/credentials/systemd-journald.service
none               1,0M            0  1,0M            0% /run/credentials/systemd-resolved.service
tmpfs               16G          44K   16G            1% /tmp
/dev/nvme0n1p2     2,0G         387M  1,5G           22% /boot
/dev/nvme0n1p3      18G         3,7G   15G           21% /home
tmpfs              3,2G         136K  3,2G            1% /run/user/1000
none               1,0M            0  1,0M            0% /run/credentials/systemd-networkd.service

total        used        free      shared  buff/cache   available
Mem:            31Gi       2,2Gi        27Gi       7,0Mi       2,1Gi        29Gi
Swap:          8,0Gi          0B       8,0Gi

USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.0  43684 22772 ?        Ss   11:35   0:01 /usr/lib/systemd/systemd --switched-root --system --deserialize=55 rhgb
root           2  0.0  0.0      0     0 ?        S    11:35   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    11:35   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-netns]
root           9  0.0  0.0      0     0 ?        I    11:35   0:00 [kworker/0:0-events]
root          12  0.0  0.0      0     0 ?        I<   11:35   0:00 [kworker/R-mm_percpu_wq]
root          14  0.1  0.0      0     0 ?        I    11:35   0:00 [kworker/u512:1-events_unbound]
root          15  0.0  0.0      0     0 ?        S    11:35   0:00 [ksoftirqd/0]
root          16  0.0  0.0      0     0 ?        I    11:35   0:00 [rcu_preempt]
root          17  0.0  0.0      0     0 ?        S    11:35   0:00 [rcu_exp_par_gp_kthread_worker/1]
```
