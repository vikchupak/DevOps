https://www.tecmint.com/list-all-running-services-under-systemd-in-linux/

`ufw` (Uncomplicated Firewall) — це зручний інструмент для управління брандмауером на базі iptables в системах на базі Linux. Його основна мета — зробити конфігурацію брандмауера простою і доступною для користувачів, які не знайомі з низькорівневими командами iptables.

### Основні можливості `ufw`:

1. **Простота використання**:
   - `ufw` (program, stabds for Uncomplicated Firewall) program for managing a ___Linux kernel's netfilter framework___. має простий синтаксис команд, що полегшує управління брандмауером.
   - `gufw` gui for`ufw`

   About Uncomplicated Firewall\
   https://en.wikipedia.org/wiki/Uncomplicated_Firewall

   About Netfilter framework\
   https://en.wikipedia.org/wiki/Netfilter

1. **Основні функції**:
   - Вмикання та вимикання брандмауера.
   - Додавання та видалення правил.
   - Відображення статусу брандмауера та поточних правил.

2. **Приклади використання**:
   ```sh
   sudo ufw enable        # Включити брандмауер
   sudo ufw disable       # Вимкнути брандмауер
   sudo ufw status        # Переглянути статус брандмауера
   sudo ufw allow 22/tcp  # Дозволити вхідний трафік на порт 22 (SSH)
   sudo ufw deny 80/tcp   # Заборонити вхідний трафік на порт 80 (HTTP)
   sudo ufw delete allow 22/tcp  # Видалити правило, яке дозволяє вхідний трафік на порт 22
   ```

3. **Інтерфейс для більш складних налаштувань**:
   - Хоча `ufw` простий у використанні, він також дозволяє налаштувати більш складні правила через редагування конфігураційних файлів.

### Новіші або альтернативні інструменти:

1. **`firewalld`**:
   - `firewalld` — це більш гнучкий і потужний інструмент для управління брандмауером, який використовує зони та служби для налаштування правил.
   - Забезпечує динамічне управління правилами, що дозволяє змінювати конфігурацію без перезапуску брандмауера.
   - Може бути використаний на системах на базі Red Hat, CentOS, Fedora та інших.

   About Firewalld\
   https://en.wikipedia.org/wiki/Firewalld

   **Graphical front-ends (GUIs)**\
   `firewall-config` is a graphical front-end that is optionally included with firewalld, with support for most of its features.

   `firewall-applet` is a small status indicator utility that is optionally included with firewalld. It can provide firewall event log notifications as well as a quick way to open firewall-config. firewall-applet was ported from the GTK+ to the Qt framework in the summer of 2015 following the GNOME Desktop’s deprecation of system tray icons.[11]

3. **Основні функції `firewalld`**:
   - Управління зонами (включення правил для різних зон безпеки).
   - Підтримка постійних і тимчасових правил.
   - Динамічне змінення правил без перезапуску сервісу.

4. **Приклади використання `firewalld`**:
   ```sh
   sudo firewall-cmd --state                     # Перевірити стан firewalld
   sudo firewall-cmd --reload                    # Перезавантажити конфігурацію firewalld
   sudo firewall-cmd --get-active-zones          # Переглянути активні зони
   sudo firewall-cmd --zone=public --add-port=22/tcp --permanent  # Додати правило для порту 22 в зону public
   sudo firewall-cmd --zone=public --remove-port=22/tcp --permanent  # Видалити правило для порту 22 в зоні public
   sudo firewall-cmd --reload                    # Перезавантажити конфігурацію для застосування постійних змін
   ```

5. **`nftables`**:
   - `nftables` — це сучасна система фільтрації пакетів, яка __замінює legacy iptables component of Netfilter___, ip6tables, arptables і ebtables.
   - Пропонує більш потужний і гнучкий синтаксис правил.

6. **Основні функції `nftables`**:
   - Спрощена структура і синтаксис правил.
   - Підтримка IPv4, IPv6, ARP і Ethernet бріджінгу в єдиній інфраструктурі.
   - Висока продуктивність та ефективність.

7. **Приклади використання `nftables`**:
   ```sh
   sudo nft list ruleset           # Переглянути поточні правила
   sudo nft add table ip filter    # Додати таблицю
   sudo nft add chain ip filter input { type filter hook input priority 0 \; }  # Додати ланцюг
   sudo nft add rule ip filter input tcp dport 22 accept  # Додати правило, що дозволяє вхідний трафік на порт 22
   ```

### Резюме:

- **`ufw`**:
  - Проста і зручна утиліта для базових потреб у налаштуванні брандмауера.
- **`firewalld`**:
  - Більш потужний і гнучкий інструмент для динамічного управління брандмауером.
- **`nftables`**:
  - Сучасна система для фільтрації пакетів з більш ефективним синтаксисом і продуктивністю.

Для більшості користувачів `ufw` буде достатньо для основних задач. Однак для більш складних і динамічних конфігурацій можна розглянути використання `firewalld` або `nftables`.
