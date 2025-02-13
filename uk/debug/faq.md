# Часті Питання

## Помилки збірки

### Переповнення Flash-пам'яті

Кількість коду, яку можна завантажити на плату, обмежується обсягом flash-пам'яті, яку вона має.
При додаванні додаткових модулів або коду можливо, що додача перевищує розмір flash-пам'яті.
Це призведе до "переповнення flash-пам'яті". Оригінальна версія завжди буде компілюватися, але залежно від того що додасть розробник вона може переповнити локально.

```sh
region `flash' overflowed by 12456 bytes
```

Для усунення цього, використовуйте новіше обладнання або видаліть модулі зі збірки, які не є необхідними для вашого випадку.
The configuration is stored in **/PX4-Autopilot/boards/px4** (e.g. [PX4-Autopilot/boards/px4/fmu-v5/default.px4board](https://github.com/PX4/PX4-Autopilot/blob/main/boards/px4/fmu-v5/default.px4board)).
Щоб видалити модуль, просто закоментуйте його:

```cmake
#tune_control
```

#### Визначення великих споживачів пам'яті

Нижче наведена команда, яка перелічить найбільші статичні виділення пам'яті:

```sh
arm-none-eabi-nm --size-sort --print-size --radix=dec build/px4_fmu-v5_default/px4_fmu-v5_default.elf | grep " [bBdD] "
```

## Помилки USB

### Завантаження ніколи не вдається

На Ubuntu видаліть менеджер модему:

```sh
sudo apt-get remove modemmanager
```
