# Конфиг iTerm2

Эта репа используется как папка настроек iTerm2. iTerm2 может читать preferences
напрямую отсюда через настройку `Load preferences from a custom folder or URL`.

## Файлы

- `com.googlecode.iterm2.plist` - полный конфиг iTerm2. Файл хранится в XML,
  поэтому его удобно читать и смотреть через `git diff`.
- `.gitignore` - исключает локальные бэкапы и временные helper-файлы.

## Настройка на новом Mac

1. Установить iTerm2.

2. Склонировать эту репу туда, где лежат остальные конфиги:

   ```sh
   git clone <repo-url> ~/dm13/configs/iterm2
   ```

3. Открыть iTerm2.

4. Перейти в:

   ```text
   iTerm2 -> Settings -> General -> Preferences
   ```

5. Включить:

   ```text
   Load preferences from a custom folder or URL
   ```

6. Выбрать папку этой репы:

   ```text
   ~/dm13/configs/iterm2
   ```

7. Перезапустить iTerm2.

После этого iTerm2 будет читать настройки из этой папки.

## Перед переключением существующего Mac

Если на текущем Mac уже есть важные настройки iTerm2, сначала сделать бэкап:

   ```sh
   cp ~/Library/Preferences/com.googlecode.iterm2.plist \
     ~/Library/Preferences/com.googlecode.iterm2.plist.backup.$(date +%Y%m%d%H%M%S) 2>/dev/null || true
   ```

После этого можно включать custom preferences folder по инструкции выше.

## Как обновлять конфиг после изменений

Когда custom preferences folder включён, iTerm2 читает и сохраняет настройки в
файл `com.googlecode.iterm2.plist` внутри этой репы.

После изменения настроек через UI iTerm2:

1. Полностью закрыть iTerm2, чтобы он записал последние изменения в plist.

2. Перейти в папку репы:

   ```sh
   cd ~/dm13/configs/iterm2
   ```

3. Проверить изменения:

   ```sh
   git status
   git diff
   ```

4. Если iTerm2 переписал plist в бинарный формат, вернуть XML-формат:

   ```sh
   plutil -convert xml1 com.googlecode.iterm2.plist
   ```

5. Ещё раз проверить diff и закоммитить изменения.

   ```sh
   git diff
   git add com.googlecode.iterm2.plist
   git commit -m "Update iTerm2 config"
   ```

## Важный биндинг

Для автокомплита в Neovim нужен key mapping в iTerm2:

- `Cmd+Shift+Space`
- действие: `Send Escape Sequence`
- текст: `[32;10u`

Это отправляет CSI-u последовательность, которую Neovim распознаёт как
`<D-S-Space>`.
