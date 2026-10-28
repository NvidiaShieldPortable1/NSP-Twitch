# NSP Twitch
Android приложение для просмотра Twitch стримов на NVIDIA SHIELD PORTABLE.
Lite Twitch client special for Nvidia Shield Portable and Android 5.1

![Screenshot](screen.png)

## 🎮 Особенности

- **Полная поддержка геймпада** NVIDIA SHIELD — навигация D-pad (←→↑↓) и кнопка A для выбора
- **Плавный скроллинг** с центрированием выбранных карточек
- **Звуковая обратная связь** при навигации
- **HLS стриминг** с автоматическим выбором качества через ExoPlayer
- **Каталог категорий** с рейтингом по количеству зрителей
- **Меню стримеров** для каждой категории с пагинацией
- **Кэширование** данных (категории 24ч, OAuth токен 55мин)
- **Полноэкранный режим** с автоматическим скрытием UI
- **Переключение качества** через меню настроек

## 📱 Требования

- Android 5.1 (API 22) и выше
- NVIDIA SHIELD PORTABLE или любое Android устройство с геймпадом
- Стабильное интернет-соединение для стриминга (используйте Wi-Fi с 5G)

## 🛠 Технологии

| Компонент | Технология |
|-----------|-----------|
| Язык | Kotlin |
| Видеоплеер | ExoPlayer (Media3) |
| Загрузка изображений | Glide |
| API | Twitch Helix API + GraphQL |
| Авторизация | OAuth 2.0 (Client Credentials Flow) |
| Минимальный SDK | 22 (Android 5.0) |
| Целевой SDK | 35 (Android 15) |

## 📦 Структура проекта

```
app/
├── src/main/java/com/example/nsptwitch/
│   └── MainActivity.kt          # Основная логика (все экраны, геймпад, плеер)
├── src/main/res/
│   ├── layout/
│   │   ├── activity_main.xml    # Макет главного экрана
│   │   ├── item_category.xml    # Карточка категории
│   │   └── item_channel.xml     # Карточка стримера
│   ├── drawable/
│   │   ├── *boxart.jpg          # Локальные иконки категорий (30 шт)
│   │   ├── category_selected_lshape.xml  # L-образная рамка выделения
│   │   └── settings_background.xml # Фон кнопок настроек
│   ├── raw/
│   │   └── click.mp3            # Звук клика при навигации
│   └── values/
│       └── strings.xml          # Строки приложения
└── build.gradle.kts             # Зависимости и конфигурация
```

## 🎯 Экраны приложения

### 1. Каталог категорий
- Сетка 5×6 (30 категорий в фиксированном порядке)
- L-образная рамка (фиолетовая #9933ff) на выбранной карточке
- Смещение выделенной карточки: +4dp X, -4dp Y
- Масштабирование выделенной карточки: 105%
- Отображение количества зрителей (если > 0)

### 2. Меню стримеров
- Сетка 3 колонки
- Превью стримов через Twitch API
- Пагинация (по 6 стримеров за раз)
- Масштабирование выделенной карточки: 102%

### 3. Плеер
- ExoPlayer с HLS поддержкой
- Кастомный контроллер (play/pause, качество, громкость, назад)
- Авто-скрытие контроллера через 3 секунды
- Автоматическое воспроизведение при возврате

## 🎮 Управление

| Клавиша | Действие |
|---------|----------|
| ← → | Навигация влево/вправо |
| ↑ ↓ | Навигация вверх/вниз |
| D-pad Center / Enter | Выбор (кнопка A) |
| Back | Назад / Свернуть |

## 🔧 Настройка

### 1. Клонирование репозитория

```bash
git clone <repository-url>
cd NSPTwitch
```

### 2. Twitch API credentials

В файле `MainActivity.kt` замените клиентские данные:

```kotlin
private const val CLIENT_ID = "your_client_id"
private const val CLIENT_SECRET = "your_client_secret"
```

Получить на [Twitch Developer Console](https://dev.twitch.tv/console)

### 3. Сборка проекта

```bash
.\gradlew.bat assembleDebug --no-daemon --console=plain
```

### 4. Установка на устройство

```bash
adb install -r "app\build\outputs\apk\debug\app-debug.apk"
```

## 📂 Кэширование

| Данные | Ключ | Время жизни |
|--------|------|-------------|
| Категории | `categories_cache` | 24 часа |
| OAuth токен | `oauth_token` | 55 минут |

## 🎨 UI/UX детали

### Карточки
- Padding: 4dp
- Margin: 4dp
- RecyclerView padding: 8dp, clipToPadding: false
- Elevation выделенной карточки: 8dp

### Цвета
- Фон: #18181b (меню), #27272a (карточки)
- Акцент: #9933ff (фиолетовый)
- Текст зрителей: #a1a1aa (серый)

### Звук
- `click.mp3` в assets, воспроизведение на 25% громкости

## 🐛 Известные ограничения

- LinearSmoothScroller может вызывать SIGSEGV на некоторых устройствах NVIDIA SHIELD при скроллинге невидимых элементов
- Голосовой поиск Twitch не поддерживается
- Требуется русскоязычный акцент (`language=ru` в запросах)

## 📄 Лицензия

MIT License

## 🤝 Вклад

PR приветствуются! Для крупных изменений откройте issue для обсуждения.

## 📬 Контакты

Вопросы и предложения — через [GitHub Issues](https://github.com/your-username/nsptwitch/issues)
