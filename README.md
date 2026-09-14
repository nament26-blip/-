Создай статический сайт-маркетплейс психологов «Равоншинос» для размещения 
на GitHub Pages с backend на Supabase.

КРИТИЧЕСКИ ВАЖНО (частые ошибки, которых нужно избежать):
1. CSS ДОЛЖЕН быть настоящим файлом с полным кодом стилей — НЕ пустой, 
   НЕ заглушка. Сайт без CSS выглядит как список слов.
2. Пути к файлам — ТОЛЬКО относительные (css/style.css, а не /css/style.css), 
   потому что сайт живёт в подпапке username.github.io/ravonshinos/.
3. Регистр имён файлов и папок: только строчные (css, js, images). 
   GitHub Pages чувствителен к регистру.
4. НЕ используй сборщики (webpack, vite, npm) — только чистый HTML/CSS/JS, 
   чтобы GitHub Pages работал без настройки.
5. Все JS-файлы подключай через <script src="js/..."></script> в конце <body>.
6. Supabase подключай через CDN.
7. НЕ используй import/export в браузерных скриптах — только window-объекты 
   или обычные <script>, иначе будет ошибка "Cannot use import statement".

НАЗВАНИЕ И СМЫСЛ:
«Равоншинос» — психолог на таджикском/персидском. Используй как бренд 
в логотипе, header, footer, title страниц и meta-тегах.
Слоган: «Найдите своего психолога».

ЯЗЫК: русский.
СТИЛЬ: спокойный, wellness-эстетика — sage green (#5A7D6A), cream (#FAF7F2), 
soft gray, скруглённые углы (border-radius 12-16px), много воздуха, 
мягкие тени. Шрифт: Inter (через Google Fonts).

═══════════════════════════════════════════════════════════
СТРУКТУРА ПРОЕКТА
═══════════════════════════════════════════════════════════

ravonshinos/
├── index.html
├── catalog.html
├── profile.html
├── login.html
├── dashboard.html
├── css/
│   └── style.css          ← ПОЛНЫЙ CSS, не пустой!
├── js/
│   ├── config.js          ← Supabase URL и anon key
│   ├── supabase-client.js ← инициализация клиента
│   ├── auth.js
│   ├── booking.js
│   └── main.js
├── assets/
│   └── images/
├── .gitignore
├── CNAME
└── README.md

═══════════════════════════════════════════════════════════
ПОДКЛЮЧЕНИЕ ФАЙЛОВ В КАЖДОМ HTML
═══════════════════════════════════════════════════════════

В <head> каждого HTML:
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="css/style.css?v=1">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Равоншинос — маркетплейс психологов</title>

В конце <body> каждого HTML:
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script src="js/config.js"></script>
<script src="js/supabase-client.js"></script>
<script src="js/main.js"></script>

═══════════════════════════════════════════════════════════
CSS (css/style.css) — ПОЛНЫЙ КОД
═══════════════════════════════════════════════════════════

* { margin: 0; padding: 0; box-sizing: border-box; }

:root {
  --sage: #5A7D6A;
  --sage-dark: #4A6D5A;
  --sage-light: #E8F0EA;
  --cream: #FAF7F2;
  --text: #2C3E35;
  --text-muted: #6B7D75;
  --white: #ffffff;
  --shadow: 0 4px 20px rgba(0,0,0,0.06);
  --shadow-hover: 0 8px 30px rgba(0,0,0,0.1);
}

body {
  font-family: 'Inter', -apple-system, sans-serif;
  background: var(--cream);
  color: var(--text);
  line-height: 1.6;
}

.container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }

header {
  background: var(--white);
  padding: 20px 0;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  position: sticky; top: 0; z-index: 100;
}
header .container { display: flex; justify-content: space-between; align-items: center; }
.logo { font-size: 24px; font-weight: 700; color: var(--sage); text-decoration: none; }
nav a { margin: 0 15px; color: var(--text); text-decoration: none; font-weight: 500; }
nav a:hover { color: var(--sage); }

.btn {
  display: inline-block; padding: 12px 24px; border-radius: 8px;
  text-decoration: none; font-weight: 600; transition: 0.3s;
  cursor: pointer; border: none; font-size: 16px;
}
.btn-primary { background: var(--sage); color: var(--white); }
.btn-primary:hover { background: var(--sage-dark); }
.btn-secondary { background: transparent; color: var(--sage); border: 2px solid var(--sage); }
.btn-secondary:hover { background: var(--sage-light); }

.hero {
  padding: 80px 0; text-align: center;
  background: linear-gradient(135deg, #F0F5F1, var(--cream));
}
.hero h1 { font-size: 48px; margin-bottom: 20px; }
.hero p { font-size: 20px; color: var(--text-muted); margin-bottom: 30px; }
.hero-buttons { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; }

.psychologists-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px; padding: 40px 0;
}
.card {
  background: var(--white); border-radius: 16px; padding: 24px;
  box-shadow: var(--shadow); transition: 0.3s;
}
.card:hover { transform: translateY(-4px); box-shadow: var(--shadow-hover); }
.card h3 { font-size: 20px; margin-bottom: 10px; }
.badge {
  display: inline-block; background: var(--sage-light); color: var(--sage);
  padding: 4px 12px; border-radius: 12px; font-size: 13px;
  margin: 4px 4px 4px 0;
}
.price { font-size: 18px; font-weight: 700; color: var(--sage); margin: 15px 0; }
.rating { color: #F5A623; margin-bottom: 15px; }

.avatar {
  width: 64px; height: 64px; border-radius: 50%;
  background: var(--sage-light); color: var(--sage);
  display: flex; align-items: center; justify-content: center;
  font-weight: 700; font-size: 22px; margin-bottom: 16px;
}

footer {
  background: var(--text); color: var(--white);
  padding: 40px 0; text-align: center; margin-top: 60px;
}

@media (max-width: 768px) {
  .hero h1 { font-size: 32px; }
  .hero p { font-size: 17px; }
  nav { display: none; }
  .psychologists-grid { grid-template-columns: 1fr; }
}

═══════════════════════════════════════════════════════════
СТРАНИЦЫ
═══════════════════════════════════════════════════════════

1. index.html — Главная:
   - Header с логотипом «Равоншинос» и навигацией.
   - Hero: «Равоншинос — найдите своего психолога», две кнопки.
   - Секция поиска с фильтрами (специализация, цена, формат).
   - «Как это работает» — 3 шага.
   - Сетка 6 карточек психологов (аватар с инициалами, имя, бейджи 
     специализаций, опыт, цена, рейтинг, кнопка «Записаться»).
   - Отзывы (3 шт).
   - CTA «Разместите профиль бесплатно».
   - FAQ.
   - Footer с «Равоншинос».

2. catalog.html — Каталог:
   - Сетка карточек (данные из Supabase, если доступен, иначе демо-данные).
   - Фильтры: специализация, цена, опыт, формат.

3. profile.html — Профиль психолога:
   - Фото/аватар, имя, квалификация, образование.
   - О себе, подходы.
   - Цена, длительность.
   - Отзывы.
   - Форма записи: имя, email, сообщение → insert в Supabase.

4. login.html — Вход:
   - Форма email → supabase.auth.signInWithOtp().
   - После входа редирект на dashboard.html.

5. dashboard.html — Кабинет клиента:
   - Список записей из таблицы bookings.
   - Email пользователя.
   - Кнопка выхода.

═══════════════════════════════════════════════════════════
JS-ФАЙЛЫ (без import/export!)
═══════════════════════════════════════════════════════════

js/config.js:
window.SUPABASE_URL = 'ВСТАВЬ_СЮДА_URL';
window.SUPABASE_ANON_KEY = 'ВСТАВЬ_СЮДА_KEY';

js/supabase-client.js:
// Глобальный клиент Supabase
window.supabaseClient = window.supabase.createClient(
  window.SUPABASE_URL,
  window.SUPABASE_ANON_KEY
);

js/auth.js:
// Функции входа/выхода через window.supabaseClient
// Использовать в login.html и dashboard.html

js/booking.js:
// Функция создания записи в таблице bookings
// Использовать в profile.html

js/main.js:
// Общая логика: рендер карточек, фильтры, мобильное меню

ВАЖНО: Никаких import/export — только window-объекты и обычные функции.

═══════════════════════════════════════════════════════════
SUPABASE: SQL-СХЕМА
═══════════════════════════════════════════════════════════

-- profiles
create table profiles (
  id uuid references auth.users primary key,
  full_name text,
  role text check (role in ('client', 'psychologist')),
  created_at timestamp with time zone default now()
);

-- psychologist_profiles
create table psychologist_profiles (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references profiles(id),
  full_name text,
  specializations text[],
  approaches text[],
  experience_years integer,
  session_price integer,
  session_duration integer,
  format text check (format in ('online','offline','both')),
  languages text[],
  education text,
  bio text,
  avatar_url text,
  rating numeric default 0,
  reviews_count integer default 0,
  is_verified boolean default false
);

-- bookings
create table bookings (
  id uuid primary key default gen_random_uuid(),
  client_id uuid references auth.users,
  psychologist_id uuid references psychologist_profiles(id),
  scheduled_at timestamp with time zone,
  duration integer,
  format text,
  status text default 'pending' check (status in ('pending','confirmed','completed','cancelled')),
  price integer,
  message text,
  created_at timestamp with time zone default now()
);

-- reviews
create table reviews (
  id uuid primary key default gen_random_uuid(),
  booking_id uuid references bookings(id),
  client_id uuid references auth.users,
  psychologist_id uuid references psychologist_profiles(id),
  rating integer check (rating between 1 and 5),
  text text,
  created_at timestamp with time zone default now()
);

-- RLS
alter table profiles enable row level security;
alter table psychologist_profiles enable row level security;
alter table bookings enable row level security;
alter table reviews enable row level security;

create policy "Public read verified psychologists"
on psychologist_profiles for select to anon, authenticated
using (is_verified = true);

create policy "Clients see own bookings"
on bookings for select to authenticated
using ((select auth.uid()) = client_id);

create policy "Clients create own bookings"
on bookings for insert to authenticated
with check ((select auth.uid()) = client_id);

create policy "Public read reviews"
on reviews for select to anon, authenticated using (true);

create policy "Users manage own profile"
on profiles for all to authenticated
using ((select auth.uid()) = id);

-- Демо-данные: 6 психологов
insert into psychologist_profiles 
(full_name, specializations, approaches, experience_years, session_price, 
 format, rating, reviews_count, is_verified, bio)
values
('Анна Иванова', ARRAY['Тревога','Депрессия'], ARRAY['КПТ'], 8, 3000, 'online', 4.9, 47, true, 'Помогаю справляться с тревогой и паническими атаками.'),
('Мария Петрова', ARRAY['Отношения','Семейная терапия'], ARRAY['Гештальт'], 12, 4500, 'both', 4.8, 63, true, 'Семейный психолог с 12-летним опытом.'),
('Дмитрий Соколов', ARRAY['Депрессия','КПТ'], ARRAY['КПТ','ACT'], 6, 2500, 'online', 4.7, 28, true, 'Работаю с депрессией и выгоранием.'),
('Елена Кузнецова', ARRAY['Детская психология'], ARRAY['Игровая терапия'], 10, 3500, 'both', 5.0, 52, true, 'Детский психолог, работаю с детьми от 3 лет.'),
('Игорь Морозов', ARRAY['Психоанализ','Тревога'], ARRAY['Психоанализ'], 15, 5000, 'offline', 4.9, 89, true, 'Психоаналитик, 15 лет практики.'),
('Ольга Новикова', ARRAY['Отношения','Самооценка'], ARRAY['КПТ','Схема-терапия'], 7, 3200, 'online', 4.8, 41, true, 'Помогаю наладить отношения с собой и другими.');

═══════════════════════════════════════════════════════════
README.md
═══════════════════════════════════════════════════════════

# Равоншинос

Маркетплейс психологов. Статический сайт на GitHub Pages + Supabase.

## Деплой на GitHub Pages

1. Создай репозиторий `ravonshinos` на github.com (Public).
2. Загрузи все файлы (кроме config.js — см. ниже).
3. Settings → Pages.
4. Source: Deploy from a branch. Branch: main. Folder: / (root).
5. Сайт: https://ваш-username.github.io/ravonshinos/

## Настройка Supabase

1. Создай проект на supabase.com (бесплатный план).
2. SQL Editor → выполни скрипт из database.sql.
3. Settings → API → скопируй Project URL и anon key.
4. Settings → API → CORS Allowed Origins добавь:
   - https://ваш-username.github.io
   - http://localhost:8000
5. Создай js/config.js локально (он в .gitignore):
   window.SUPABASE_URL = 'твой-url';
   window.SUPABASE_ANON_KEY = 'твой-anon-key';

## Кастомный домен

1. Файл CNAME в корне с одной строкой: ravonshinos.tj
2. DNS у регистратора:
   A-записи для @:
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
   CNAME для www: ваш-username.github.io
3. Settings → Pages → Enforce HTTPS.

## Проверка после деплоя

- Открой DevTools (F12) → Console: не должно быть ошибок 404.
- Network → style.css должен загружаться со статусом 200.
- Если сайт выглядит как список слов — проверь, что style.css 
  не пустой и путь к нему относительный.

═══════════════════════════════════════════════════════════
.gitignore
═══════════════════════════════════════════════════════════

js/config.js
.DS_Store
node_modules/

═══════════════════════════════════════════════════════════
КОНЕЦ ПРОМТА
═══════════════════════════════════════════════════════════

Сгенерируй ВСЕ файлы полностью, с реальным рабочим кодом, 
без заглушек "// TODO" и "/* стили */". CSS должен быть длинным 
и полным. HTML — валидным. JS — рабочим без import/export.
