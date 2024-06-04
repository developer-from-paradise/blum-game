
# Blum

Blum клон игры

Это простая игра на Pygame, в которой нужно нажимать на падающие звезды, чтобы получить очки. Избегайте нажатия на падающие бомбы, иначе ваши очки будут уменьшены.

## Установка

1. Убедитесь, что у вас установлен Python.
2. Установите Pygame, если он еще не установлен:

   ```bash
   pip install pygame
   ```

3. Скачайте и разместите изображения `star.png`, `bomb.png` и `background.png` в той же директории, что и этот скрипт.

## Запуск игры

Запустите игру с помощью следующей команды:

```bash
python3 имя_файла.py
```

где `имя_файла.py` - это имя вашего файла со скриптом игры.

## Как играть

- Нажимайте на падающие звезды, чтобы получать очки.
- Избегайте нажатия на падающие бомбы, иначе ваши очки уменьшатся на 100 (минимум 0 очков).
- Игра продолжается 30 секунд. После окончания времени игра заканчивается и отображается ваш счет.
- Для перезапуска игры нажмите Enter.

## Описание кода

### Инициализация Pygame

```python
pygame.init()
```

Инициализация Pygame.

### Настройки окна

```python
screen_width = 460
screen_height = 725
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Blum")
```

Настройки размера окна и его заголовка.

### Загрузка изображений

```python
star_image = pygame.image.load("star.png")
bomb_image = pygame.image.load("bomb.png")
background_image = pygame.image.load("background.png")
```

Загрузка изображений для звездочек, бомб и фона.

### Классы объектов

#### Класс `Star`

Этот класс описывает звездочку, которая падает с верхней части экрана.

```python
class Star(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        size = random.randint(20, 40)
        self.image = pygame.transform.scale(star_image, (size, size))
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, screen_width - self.rect.width)
        self.rect.y = -self.rect.height
        self.speed = random.randint(3, 7)

    def update(self):
        self.rect.y += self.speed
        if self.rect.top > screen_height:
            self.kill()
```

#### Класс `Bomb`

Этот класс описывает бомбу, которая также падает с верхней части экрана.

```python
class Bomb(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.transform.scale(bomb_image, (24, 32))
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, screen_width - self.rect.width)
        self.rect.y = -self.rect.height
        self.speed = random.randint(3, 7)

    def update(self):
        self.rect.y += self.speed
        if self.rect.top > screen_height:
            self.kill()
```

### Основной игровой цикл

Функция `game_loop()` содержит основной игровой цикл, который управляет логикой игры.

### Конец игры

После окончания времени отображается счет, и игроку предлагается нажать Enter для перезапуска игры.

### Запуск игрового цикла

```python
game_loop()
```

Запуск основного игрового цикла.
