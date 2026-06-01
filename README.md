# 🚀 Запуск трекера "Июнь отжиманий" — пошагово

Сайт уже работает из коробки в **демо-режиме** (данные хранятся в браузере у каждого отдельно). Чтобы все 4 участника видели общий прогресс — подключите Firebase. Это бесплатно и занимает ~10 минут.

---

## Шаг 1. Откройте `index.html` локально и проверьте

Откройте `index.html` двойным кликом в браузере. Убедитесь, что:
- Видна шапка "Челлендж Июнь отжиманий"
- Есть карточки участников: Евгений, Папа, Лев, Глеб
- Есть форма ввода и календарь

Если всё ок — идём дальше.

---

## Шаг 2. Создайте бесплатный Firebase-проект

1. Зайдите на **https://console.firebase.google.com** (логин через Google).
2. Нажмите **"Add project"** → имя любое (например, `pushup-challenge`).
3. Google Analytics — можно отключить, не нужен.
4. После создания нажмите **"Build" → "Realtime Database"** в левом меню.
5. Нажмите **"Create Database"** → регион **`europe-west1`** (Бельгия, ближе всего к РФ).
6. Стартовый режим выберите **"Start in test mode"** (правила доступа на 30 дней — нам как раз хватит).

---

## Шаг 3. Получите Firebase config

1. В Firebase Console нажмите ⚙️ (шестерёнка вверху слева) → **"Project settings"**.
2. Прокрутите вниз до **"Your apps"** → нажмите иконку **`</>`** (Web).
3. Введите nickname (любое), **не** включайте Firebase Hosting → Register app.
4. Скопируйте объект `firebaseConfig` — он будет такого вида:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "pushup-challenge.firebaseapp.com",
  databaseURL: "https://pushup-challenge-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "pushup-challenge",
  storageBucket: "pushup-challenge.appspot.com",
  messagingSenderId: "...",
  appId: "..."
};
```

---

## Шаг 4. Вставьте config в `index.html`

Откройте `index.html` в любом редакторе (Блокнот, VS Code). Найдите блок:

```html
<!-- ============== FIREBASE CONFIG ============== -->
```

И **раскомментируйте** строки (уберите `//` в начале):

```js
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getDatabase, ref, set, onValue } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-database.js";

const firebaseConfig = {
  apiKey: "ВАШ_API_KEY",     // ← подставьте свои значения
  authDomain: "...",
  databaseURL: "...",
  // ...
};
const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
window.__fb = { db, ref, set, onValue };
```

Сохраните файл. Откройте — должна быть зелёная плашка **"✅ Облако подключено"**.

---

## Шаг 5. Выложите сайт на GitHub Pages (бесплатно навсегда)

1. Регистрируйтесь на **https://github.com** (если ещё нет аккаунта).
2. Нажмите **"+ → New repository"** → имя `pushup-june` → **Public** → Create.
3. На странице репозитория нажмите **"uploading an existing file"** → перетащите `index.html` → Commit.
4. Зайдите в **Settings → Pages** (в меню репозитория).
5. В разделе "Build and deployment": **Source: Deploy from a branch**, **Branch: main / (root)** → Save.
6. Через 1–2 минуты сайт будет доступен по адресу:
   **`https://ВАШ_ЛОГИН.github.io/pushup-june/`**

Скиньте эту ссылку папе, Льву и Глебу — все вносят прогресс с любого устройства, всё синхронизируется.

---

## Шаг 6 (важно). Защита данных

В режиме "test mode" база открыта на 30 дней — это нам ок, как раз срок челленджа. Если хочется усилить:

1. Firebase Console → Realtime Database → Realtime Database **"Rules"**.
2. Замените на:
```json
{
  "rules": {
    "challenge2026june": {
      ".read": true,
      ".write": true
    }
  }
}
```

Это разрешит читать-писать только нашу ветку, остальное закрыто.

---

## Альтернатива GitHub Pages — Netlify Drop

Если GitHub кажется сложным:
1. Зайдите на **https://app.netlify.com/drop**.
2. Перетащите `index.html` в окно браузера.
3. Получите ссылку вида `https://xxx.netlify.app` — готово.

---

## Что куда вводить — для семьи

📱 Когда участник заходит первый раз:
1. В карточке со своим именем вводит **стартовый уровень** (сколько отжиманий может сделать сейчас, 1 июня).
2. Каждый день в форме ввода: выбирает себя → выбирает день → пишет результат → опционально ссылку на видео (с Телеги/Ютуба) → "Сохранить".

🎬 Видеоотчёт:
- Сними видео в Телеге → отправь в избранное → нажми "Скопировать ссылку на сообщение" → вставь в трекер.
- Или загрузи в YouTube как "Доступ по ссылке" → скопируй ссылку.

🏆 30 июня смотрим в таблицу лидеров — у кого число справа выше, тот забирает 8 000 ₽.

---

Удачи в челлендже! 💪

