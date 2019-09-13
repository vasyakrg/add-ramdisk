# Create Ramdisk to debain

## Описание
- плейбук создает RAM-диск, отрезая у ОЗУ немного места.
- можно использовать для монтировать в виртуалки, в те места, где необходима супер-скорость и неважен стейт данных.
- например для кеширования.


### Предварительные требования (для Mac OS)
- [Ansible](https://docs.ansible.com)
  > brew install ansible

####
- перезапуском не забыть обновить роли!
  > ansible-galaxy install -r requirements.yml -f

#### Работа со скриптом:
  > cd ansible && ansible-playbook init.yml

#### Что делается фактически:
- mkdir /tmp/ramdisk
- chmod 777 /tmp/ramdisk
- mount -t tmpfs -o size=1024m myramdisk /tmp/ramdisk

#### Как тестировать?
- проверить запись в ОЗУ-диск
  > sudo dd if=/dev/zero of=/tmp/ramdisk/zero bs=4k count=100000

- для сравнение проверить записи в текущий диск
  > sudo dd if=/dev/zero of=/tmp/zero bs=4k count=100000

- проверка на чтение с ОЗУ-диска
  > sudo dd if=/tmp/ramdisk/zero of=/dev/null bs=4k count=100000

- чтение с обычного диска
  > sudo dd if=/tmp/zero of=/dev/null bs=4k count=100000

#### Перед запуском не забыть обновить роли!
  > ansible-galaxy install -r requirements.yml


#### Как я все это делал
- Видео с подробными инструкциями доступно [тут]()

##### Автор
- **Vassiliy Yegorov** - *Initial work* - [vasyakrg](https://github.com/vasyakrg)
- [сайт](vk.com/realmanual)
- [youtube](youtube.com/realmanual)
