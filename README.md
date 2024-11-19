# dhcpdLogsScan

Этот скрипт предназначен для обработки логов DHCP-сервера и извлечения новых MAC-адресов, которые ранее не были обработаны.

---

## 📋 Описание работы

Скрипт выполняет следующие функции:

1. **Чтение обработанных MAC-адресов**  
   Извлекает данные из CSV-файла (`MACs.csv`), чтобы избежать повторной обработки уже известных адресов.

2. **Анализ логов DHCP**  
   Находит новые MAC-адреса в файле логов (`dhcpd.log`), которые не содержатся в списке обработанных.

3. **Сохранение новых MAC-адресов**  
   Записывает новые адреса в файл `new_macs.txt` с указанием времени их обнаружения.

---

## 🗂️ Структура файлов

- **`dhcpd.log`**  
  Лог-файл DHCP-сервера с данными о запросах.  

- **`MACs.csv`**  
  CSV-файл с обработанными MAC-адресами. Обязательная колонка: `MACAddress`.

- **`new_macs.txt`**  
  Файл для сохранения новых MAC-адресов с отметками времени.

---

## 🔧 Настройка
Пути к файлам задаются переменными:

- **`LOG_FILE`**  
  Путь к файлу логов DHCP-сервера (`dhcpd.log`).

- **`PROCESSED_MACS_FILE`**  
  Путь к файлу обработанных MAC-адресов (`MACs.csv`).

- **`NEW_MACS_FILE`**  
  Путь к файлу для сохранения новых MAC-адресов (`new_macs.txt`).

---

## 🛠️ Функции

- **`read_processed_macs()`**  
Читает MAC-адреса из CSV-файла и сохраняет их в список processed_macs_from_file.

- **`extract_mac_addresses(log_file)`**  
Извлекает новые MAC-адреса из логов DHCP-сервера и возвращает их в формате:
  `Time: <время>, MAC: <адрес>`.

- **`main()`**  
Считывает обработанные MAC-адреса.
Находит новые MAC-адреса в логах.
Сохраняет новые адреса в файл и выводит их количество в консоль.

---

## 📝 Пример логов
Пример строки из файла `dhcpd.log`:  
`Nov 18 15:23:47 dhcp-freebsd-pxe dhcpd[1147]: DHCPDISCOVER from 00:1a:2b:3c:4d:5e via re0`

---

## ℹ️ Примечания
- Если файл `MACs.csv` отсутствует, скрипт начнёт с пустого списка обработанных адресов.
- Если новых MAC-адресов не найдено, файл `new_macs.txt` не создаётся.
- Пути к файлам имеет смысл дополнительно редактировать для удобства использования.
- Перед каждым запуском скрипта заносите обработанные MAC-адреса в `.csv` файл для корректного учета.

---

## 📜 Лицензия
Скрипт предоставляется "как есть". Убедитесь, что его использование соответствует вашим требованиям.
