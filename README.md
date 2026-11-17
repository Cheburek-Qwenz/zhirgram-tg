# ZhirGram

Клиент Telegram для Android: патчсет поверх стокового Telegram на основе [Inugram](https://github.com/teidesu/inugram)
(MIT) с собственными доработками. Цель: настоящий Material 3 и Material 3 Expressive.

Рабочее название, пакет `com.qwenz.zhirgram`. Статус и задачи: [AGENTS.md](AGENTS.md).
**Эта сборка ещё ни разу не запускалась в CI.** Список функций Inugram: [FEATURES.md](FEATURES.md).

## Как собрать (GitHub Actions)

1. Settings → Secrets and variables → Actions, секреты `TG_APP_ID` и `TG_APP_HASH` (my.telegram.org).
2. Actions → **Build ZhirGram** → Run workflow. Сборка 30-90 минут.
3. APK в Artifacts: `gh run download -n zhirgram-apk`.

Подпись пока debug-ключом, обновлять поверх можно только сборкой, подписанной тем же ключом.

## Как посмотреть настоящий код Telegram

Actions → **Export stock files**: в поле paths пути внутри worktree, на выходе `files.zip`. Нужно, чтобы
писать патчи с точным контекстом (без исходников Telegram под рукой патчи писать вслепую нельзя).

## Лицензии

GPL v2+ (Telegram), MIT (Inugram). См. [ATTRIBUTION.md](ATTRIBUTION.md).
