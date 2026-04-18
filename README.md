# VLF для Linux

VPN-клиент на базе sing-box с поддержкой VLESS / Reality / Hysteria2 / Trojan / VMess, TUN-режимом и автоматической маршрутизацией RU/GLOBAL.

- **Версия:** 1.2.31
- **Поддерживаемые дистрибутивы:** Ubuntu 20.04+, Debian 11+, любые deb-совместимые с GTK 3
- **Архитектура:** x86_64 (amd64)

## Установка

### Через .deb (рекомендуется)

```bash
sudo apt install ./vlf_1.2.31_amd64.deb
```

или

```bash
sudo dpkg -i vlf_1.2.31_amd64.deb
sudo apt-get install -f   # доустановит зависимости, если понадобится
```

Приложение появится в меню как **VLF**. Команда запуска из терминала — `vlf`.

### Зависимости

Устанавливаются автоматически менеджером пакетов:

- `libgtk-3-0`
- `libstdc++6`
- `libayatana-appindicator3-1` (или `libappindicator3-1`)
- `libcap2-bin`

Для Ubuntu 24.04 и новее `libayatana-appindicator3-1` берётся из `universe` — при необходимости включите его:
```bash
sudo add-apt-repository universe
sudo apt update
```

## Первый запуск

При установке через `.deb` postinst автоматически:

1. Выдаёт `sing-box` капабилити `CAP_NET_ADMIN` + `CAP_NET_RAW` — TUN поднимается без `sudo`.
2. Прописывает polkit-правило, разрешающее `systemd-resolved` настраивать DNS на TUN-интерфейсе без пароля (действует только для активной локальной сессии).
3. Прописывает udev-правило (`NM_UNMANAGED=1`) и keyfile для NetworkManager, чтобы NM не пытался переконфигурировать интерфейс `vlf-tun`.

В результате подключение VPN **не запрашивает пароль** ни одного раза.

## Portable-запуск (без установки)

Можно распаковать тарбол и запустить `./vlf_dart` из папки. На первом старте TUN-режима появится **одно** окно polkit с паролем — bootstrap скрипт `vlf-grant-perms.sh` выполнит все те же действия, что и postinst. На последующих запусках пароль больше не запрашивается.

## Сборка из исходников

### Зависимости для сборки

```bash
sudo apt install flutter clang cmake ninja-build pkg-config \
  libgtk-3-dev libayatana-appindicator3-dev libcap2-bin \
  libblkid-dev liblzma-dev
```

Также нужен Go 1.21+ для сборки `sing-box` (если не используете pre-built бинарь из `assets/core/`).

### Сборка .deb

```bash
git clone https://github.com/<owner>/vlf_dart.git
cd vlf_dart
git submodule update --init --recursive
bash tools/build_linux_deb.sh --release
```

Готовый пакет появится в `release/linux/vlf_<version>_amd64.deb`.

## Решение проблем

### «Ошибка: sing-box не найден»
Проверьте, что `.deb` установлен: `dpkg -l | grep vlf`. В portable-режиме убедитесь, что `sing-box` лежит рядом с `vlf_dart` или в `assets/core/sing-box-linux-amd64`.

### При старте TUN всё равно спрашивает пароль
Убедитесь, что polkit-правило на месте:
```bash
ls /usr/share/polkit-1/rules.d/50-io.vlf.tunnel.rules
```
Если файла нет — переустановите пакет (`sudo apt install --reinstall ./vlf_1.2.31_amd64.deb`). На headless/SSH-сессиях пароль будет запрашиваться всегда: правило сработает только при `subject.active && subject.local`.

### Трей-иконка не отображается
На GNOME 42+ нужен `gnome-shell-extension-appindicator`:
```bash
sudo apt install gnome-shell-extension-appindicator
```
После установки перелогиньтесь.

### Нет доступа к веб-страницам после подключения
Проверьте маршрут по умолчанию: `ip route show default`. Если `vlf-tun` не основной — пересоздайте подключение в настройках VLF (включите «Глобальный VPN» либо добавьте домен в исключения).

## Удаление

```bash
sudo apt remove vlf      # оставит пользовательские настройки
sudo apt purge vlf       # полное удаление + системные конфиги polkit/udev/NM
```

## Лицензии

Клиент собран на базе:
- [sing-box](https://github.com/SagerNet/sing-box) — GPL-3.0
- [sing-tun](https://github.com/SagerNet/sing-tun) — GPL-3.0
- [xray-core](https://github.com/XTLS/Xray-core) — MPL-2.0 (опционально)

## Что нового в 1.2.31

- Исправлены три polkit-запроса пароля при старте TUN (DNS, домены, default-route) — теперь подключение проходит молча.
- Устройство `vlf-tun` помечается как `NM_UNMANAGED` на уровне udev — NetworkManager больше не пытается его переконфигурировать.
- Улучшена логика обновления подписок (правильно исчезают удалённые серверы, сразу появляются новые).
- Обход HTTP-кеша CDN для подписок через cache-busting и `Cache-Control: no-store`.
- Добавлен переключатель профилей в шапке десктопного UI.
