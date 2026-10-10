# Softy Pinko — Docker

مشروع Docker: نبني تطبيق ويب من عدة حاويات، خطوة بخطوة، من صورة بسيطة
إلى تطبيق كامل خلف proxy مع موازنة حِمل.

## المفاهيم

| المفهوم | الشرح |
| --- | --- |
| `Dockerfile` | وصفة بناء الصورة: من أي صورة نبدأ، وش نثبّت، وش نشغّل |
| `FROM` | الصورة الأساس (ubuntu, nginx…) |
| `RUN` | أمر يُنفَّذ **وقت البناء** ويصير طبقة في الصورة |
| `CMD` | الأمر الافتراضي الذي يُنفَّذ **وقت تشغيل** الحاوية |
| `WORKDIR` / `COPY` | مجلد العمل داخل الصورة، ونسخ ملفات من جهازك إليها |
| `-p 5252:5252` | ربط منفذ الحاوية بمنفذ الجهاز |
| `docker-compose.yml` | تعريف عدة خدمات وتشغيلها كلها بأمر واحد |
| DNS الداخلي | داخل compose تنادي الخدمة باسمها مثل `http://back-end:5252` |
| Proxy (`proxy_pass`) | سيرفر واحد في الواجهة يوزّع الطلبات على الخدمات خلفه |
| `--scale` | تشغيل أكثر من نسخة من نفس الخدمة، و Nginx يوزّع بينها Round-Robin |

## المهام

| المجلد | المحتوى |
| --- | --- |
| `task0` | أول صورة: ubuntu + apt update/upgrade، تطبع `Hello, World!` |
| `task1` | إضافة python3 و pip3 و flask، وسيرفر `api.py` على المنفذ 5252 |
| `task2` | فصل المشروع إلى `back-end` و `front-end` (Nginx على 9000) |
| `task3` | ربط الواجهة بالـ API عبر AJAX + تفعيل CORS في Flask |
| `task4` | `docker-compose.yml` يشغّل الخدمتين معاً |
| `task5` | إضافة خدمة `proxy` على المنفذ 80، وإخفاء منافذ الخدمات الداخلية |
| `task6` | توسيع أفقي: نسختان من `back-end` مع موازنة حِمل |

## أوامر التشغيل

```bash
# task0
docker build -f ./Dockerfile -t softy-pinko:task0 .
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0

# task1
docker build -f ./Dockerfile -t softy-pinko:task1 .
docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
curl http://localhost:5252/api/hello

# task2 / task3 (صورتان منفصلتان)
docker build -f ./back-end/Dockerfile  -t softy-pinko-back-end:task3  ./back-end
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
docker run -p 5252:5252 -it --rm softy-pinko-back-end:task3
docker run -p 9000:9000 -it --rm softy-pinko-front-end:task3

# task4 و task5
docker-compose build
docker-compose up

# task6 — نسختان من الـ API
docker-compose up --scale back-end=2
```

بعد `task5` كل شيء يمر عبر المنفذ 80: الصفحة على `http://localhost`
والـ API على `http://localhost/api/hello`.
