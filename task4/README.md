# Task 4 — Making it Simpler with Docker Compose

بدل بناء وتشغيل كل صورة يدوياً في طرفية منفصلة، نعرّف كل الخدمات في ملف
`docker-compose.yml` ونشغّلها بأمر واحد.

## ما يختصره Compose

| يدوياً | بـ Compose |
| --- | --- |
| `docker build` لكل خدمة | `docker-compose build` |
| `docker run` في طرفية لكل حاوية | `docker-compose up` |
| تمرير `-p` و `--name` في كل مرة | مكتوبة مرة واحدة في الملف |

## أقسام كل خدمة

- `build.context` و `build.dockerfile` — من أين ومن أي ملف نبني
- `image` — اسم ووسم الصورة الناتجة
- `ports` — ربط منافذ الحاوية بالجهاز
- `depends_on` — ترتيب الإقلاع

```bash
docker-compose build
docker-compose up
```
