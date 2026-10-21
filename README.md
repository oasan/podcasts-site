# Сайт приложения «Подкасты»

Публичная страница приложения и его политика конфиденциальности.
Структура — как у сайта «Аудиокниг» (`~/Developer/personal/audiobookplayer/site`).
Публикуется через GitHub Pages из ветки `main`, папка `/ (root)`:
https://oasan.github.io/podcasts-site/

- `index.html` — лендинг. Стили, палитры всех тем (роли из `Color.kt`
  приложения) и скрипт — внутри файла.
- `img/<палитра>-<фон>/*.webp` — снимки экранов, шесть тем, 600 px
  по ширине. Делаются из PNG в `screenshots/` (см. ниже).
- `fonts/` — Golos Text и JetBrains Mono, вариативные, OFL.
- `privacy.html` — политика конфиденциальности. После того как адрес указан
  в Play Console — **не переименовывать и не переносить**. Единственный
  источник текста политики — этот файл.
- `assets/style.css`, `assets/icon.webp` — стили и значок страницы политики.
- `.nojekyll` — отключает обработку Jekyll на GitHub Pages.

## Скриншоты

`screenshots/` — исходные PNG 2160 × 4848 (≈ 290 МБ), карта — в
`screenshots/README.md`. **Не публикуются**: папка исключена в `.gitignore`.

Пересобрать webp для кадров, которые использует страница:

```
for t in cool warm; do for b in light dark black; do
  for f in img/$t-$b/*.webp; do s=$(basename $f .webp)
    cwebp -quiet -q 80 -resize 600 0 screenshots/$t/$b/$s.png -o $f
  done
done; done
```

Новый кадр — сначала создать его webp во всех шести папках, потом
сослаться на него в `index.html` по имени без расширения (`data-shot`).

## Скачивание

Кнопки «Скачать APK» в `index.html` ведут на последнюю сборку в GitHub Releases:
https://github.com/oasan/podcasts-site/releases/latest/download/podcasts.apk

Публикация новой сборки:

1. Проверить версию и подпись релизного APK (`../releases/`).
2. Создать релиз с тегом `v<versionName>.<versionCode>` (например, `v1.0.7`)
   и описанием изменений.
3. Прикрепить APK с постоянным именем **`podcasts.apk`**.
4. Опубликовать релиз и отметить его как **Latest**.
5. Обновить подпись версии в обеих кнопках (`small.version`, `v 1.0.7`)
   в `index.html` и опубликовать сайт. Адрес скачивания остаётся прежним.

APK прикрепляется к релизу, в Git его не добавлять. AAB и `mapping.txt`
хранятся локально в `../releases/`.

Локальный просмотр: `python3 -m http.server 8000` из этой папки.

Репозиторий публичный: ничего закрытого сюда не класть.
