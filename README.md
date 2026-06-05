CleanPC — Руководство по сборке
Десктопное приложение для очистки и оптимизации Windows. Построено на Electron + React + Vite.
Требования
Инструмент	Версия	Ссылка
Node.js	18 LTS или новее	https://nodejs.org
npm	входит в Node.js	—
> PostgreSQL **не нужен**. Приложение работает полностью офлайн, данные хранятся локально.
---
Быстрый старт (разработка)
```powershell
# 1. Установить зависимости фронтенда
cd artifacts/cleaner-app
npm install

# 2. Установить зависимости Electron
cd ../../electron
npm install

# 3. Собрать фронтенд
cd ../artifacts/cleaner-app
npm run build

# 4. Запустить приложение
cd ../../electron
npm start
```
---
Сборка установщика
```powershell
cd electron
node build.mjs --package
```
Готовый инсталлятор появится в `electron/dist-installer/CleanPC Setup 1.0.0.exe`.
Время сборки: ~2–4 минуты.
---
Структура проекта
```
artifacts/cleaner-app/   # React-фронтенд (Vite + Tailwind)
  src/
    App.jsx              # Главный компонент
    App.css              # Глобальные стили
    main.jsx             # Точка входа React

electron/                # Electron-обёртка
  src/
    main.js              # Главный процесс
    preload.js           # Мост между процессами (contextBridge)
  assets/
    icon.ico             # Иконка приложения
    license.txt          # Лицензия для установщика
  app/frontend/          # Собранный фронтенд (генерируется build.mjs)
  build.mjs              # Скрипт сборки
  package.json
```
---
Расположение данных приложения
Данные	Путь
Логи	`%AppData%\CleanPC\logs\`
Настройки	`%AppData%\CleanPC\usercfg.json`
---
Устранение неполадок
Проблема	Решение
`icon.ico not found`	Поместите `icon.ico` в `electron/assets/`
Фронтенд не найден	Выполните `npm run build` в `artifacts/cleaner-app`
Ошибки сборки	Запустите `npm install` в обеих папках
Открываются DevTools	Уберите флаг `--dev` при запуске
---
Разработка
Для запуска с DevTools:
```powershell
cd electron
npm start -- --dev
```
