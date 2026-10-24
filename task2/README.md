# Task 2 — Front-end

نفصل المشروع إلى `back-end` و `front-end`، ونضيف خادماً ثابتاً للواجهة
باستخدام **Nginx**.

## البنية

```
task2/
├── back-end/      Dockerfile + api.py        (Flask على 5252)
└── front-end/     Dockerfile + conf + الموقع (Nginx على 9000)
```

## نقاط مهمة

- صورة الواجهة تبدأ من `nginx:latest` لا من `ubuntu` — Nginx مثبّت مسبقاً.
- ملفات الموقع تُنسَخ إلى `/var/www/html/softy-pinko-front-end`.
- ملف الإعداد يُنسَخ إلى `/etc/nginx/conf.d/default.conf` بالضبط — هذا
  المسار هو ما يقرأه Nginx افتراضياً.
- قسم `server` في الإعداد يحتاج: `listen` و `server_name` و `root` و `index`.

```bash
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
docker run -p 9000:9000 -it --rm softy-pinko-front-end:task2
```
