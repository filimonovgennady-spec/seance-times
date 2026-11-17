# DESIGN.md — The Séance Times

Дизайн-система газеты. Источник правды — `assets/site.css` и `tools/render.py`; этот файл описывает её словами, чтобы ИИ-агент собирал материалы в стиле издания.

## Палитра

| Токен | HEX | Где применять |
|---|---|---|
| `paper` | `#f4f0e5` | фон страницы, «бумага» |
| `paper-2` | `#efe9da` | врезки, подложки, чередование полос |
| `ink` | `#181410` | основной текст, линейки, заголовки |
| `ink-soft` | `#3a332a` | подзаголовки, лид |
| `muted` | `#5e5546` | подписи, даты, источники |
| `rule` | `#181410` | линии-волоски, границы блоков |
| `hair` | `rgba(24,20,16,.28)` | тонкие разделители |
| `accent` | `#8a1b1b` | один акцент: рубрика, ссылка, метка |
| `accent-soft` | `#a8453f` | ховер акцента |

Правило: **один акцент на экран**. Никаких градиентов, теней и «стекла». Цвет — только из таблицы.

## Типографика

| Роль | Шрифт | Размер | Начертание |
|---|---|---|---|
| Заголовок номера | `Playfair Display`, Iowan Old Style, Palatino, Georgia, serif | `clamp(2.15rem, 8.6vw, 5.9rem)` | 400–800, `letter-spacing: .02em` |
| Заголовок материала | тот же display | `clamp(1.4rem, 3.4vw, 2.2rem)` | 800, `line-height 1.03` |
| Текст | `Lora`, Iowan Old Style, Georgia, serif | 17.5–18px | 400, `line-height 1.62` |
| Лид | Lora italic | `clamp(.9rem, 2.4vw, 1.15rem)` | italic |
| Служебное (рубрики, даты, источники) | `Segoe UI`, system-ui, Helvetica, Arial, sans-serif | .68–.7rem | uppercase, `letter-spacing .14–.2em` |

Мера строки: `--measure: 34rem` (≈68 знаков). Длиннее — ошибка вёрстки.

## Сетка и ритм

- Одна колонка, максимум ширины — по `--measure`; широкие блоки (врезка, галерея) выходят за меру и выравниваются по краю.
- Вертикальный ритм держится на линиях-волосках `1px` цвета `rule`/`hair`, а не на отступах-пустотах.
- Шапка: надзаголовок «THE» отдельной строкой, `letter-spacing .5em`, `text-indent .5em`.
- Полоса выпуска (дата, номер) — uppercase sans, ось по левому краю текста.

## Чего не бывает

- Градиентов, `box-shadow`, размытий, скруглений больше 2px.
- Эмодзи в тексте и заголовках.
- Плоского клипарта и стоковых иконок.
- Больше одного акцентного цвета на блок.
- Таблиц в теле материала (только в служебных сводках).

## CSS-переменные (копировать как есть)

```css
:root{
  --paper:#f4f0e5; --paper-2:#efe9da;
  --ink:#181410; --ink-soft:#3a332a; --muted:#5e5546;
  --rule:#181410; --hair:rgba(24,20,16,.28);
  --accent:#8a1b1b; --accent-soft:#a8453f;
  --measure:34rem;
  --display:'Playfair Display','Iowan Old Style','Palatino Linotype',Palatino,Georgia,serif;
  --serif:'Lora','Iowan Old Style',Georgia,'Times New Roman',serif;
  --sans:'Segoe UI',system-ui,-apple-system,'Helvetica Neue',Arial,sans-serif;
}
```

## Изображения

Только свободные источники (Wikimedia Commons, NASA), скачанные локально в `assets/img/`, пережатые в JPEG, ширина ≤1600px. Исходники — в `assets/_src/` (не публикуется). Подпись и источник обязательны.
