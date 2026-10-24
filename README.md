# XML-AGR для Revit — релизы надстроек

Здесь публикуются сборки надстроек **XML-AGR IDS** и **XML-AGR Зоны** для Autodesk Revit 2019, 2023, 2024, 2025
(авторский проект «Лисья Таверна»):

* **XML-AGR IDS** — проверка моделей по IDS, проверка маппинга, анализ «СтроимПросто», АГР-утилиты (корпуса и секции, коды МССК, ТЭП, имена планов), справка.
* **XML-AGR Зоны** — проверка границ зон (Area) и кодов МССК помещений.

## Как установить

1. Откройте раздел **Releases** и скачайте архив нужного плагина (`XML-AGR-IDS-Revit-CSharp-<версия>.zip` или `XML-AGR-Zones-Revit-CSharp-<версия>.zip`).
2. Закройте Revit. Перед распаковкой: ПКМ по архиву → Свойства → «Разблокировать» (иначе Revit 2019–2024 может не загрузить DLL).
3. Распакуйте архив и запустите `install.cmd` — надстройка копируется в `%APPDATA%\Autodesk\Revit\Addins\<год>\`.
4. Запустите Revit. При первом запуске подтвердите загрузку неподписанной надстройки («Всегда загружать»).

## Как обновляться

В Revit: вкладка **XML-AGR IDS → О панели → «Обновления»**. Кнопка «Проверить» читает файл
[`latest.json`](latest.json) из этого репозитория (обычный HTTP GET, ничего о вас и модели не отправляется;
автоматической проверки при запуске Revit нет). «Скачать и установить» загружает архив, сверяет SHA-256 с `latest.json`
и ставит обновление **после закрытия Revit** — пока Revit открыт, файлы надстроек заняты. Журнал установки:
`%LOCALAPPDATA%\XML-AGR\updates\install.log`.

Разрешены только адреса `github.com/Smailkiller/…` и `raw.githubusercontent.com/Smailkiller/…` по https.

## Для автора: как выпустить версию

1. Соберите плагин (`build.ps1` в папке плагина) — появится `dist\…-<версия>.zip`.
2. `powershell -ExecutionPolicy Bypass -File ПЛАГИНЫ\Revit\tools\make_update_manifest.ps1 -IdsNotes notes-ids.md -ZonesNotes notes-zones.md` —
   формирует `latest.json` и `release-notes\`. Выпуск одного плагина: `-Only Ids` или `-Only Zones` (второй берётся из текущего `latest.json`).
3. На GitHub создайте релиз с тегом `ids-v<версия>` / `zones-v<версия>`, приложите zip, затем закоммитьте `latest.json` в `main`.

Формат `latest.json`: `{"schema":1,"plugins":{"XmlAgrIds":{"title","version","url","sha256","size","notes","date"},"XmlAgrZones":{…}}}`.

## Ссылки

* Telegram-сообщество XML-AGR — <https://t.me/xmlagr>
* «Лисья Таверна», авторский канал о BIM — <https://t.me/SMailsPub>

Результаты автоматических проверок рекомендуется перепроверять в контексте проекта.
