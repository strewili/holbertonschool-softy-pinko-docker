# Task 3 — Connecting the Front-end and Back-end

نربط الواجهة بالـ API: الصفحة تطلب `/api/hello` بـ AJAX وتعرض الناتج في
`<h1 id="dynamic-content">`.

## نقاط مهمة

- **CORS** — الواجهة على المنفذ 9000 والـ API على 5252، فهما **أصلان
  مختلفان** من وجهة نظر المتصفح. بدون `flask-cors` يحجب المتصفح الطلب
  ويظهر خطأ في الـ console رغم أن السيرفر يرد بشكل سليم.
- الإصلاح سطران في `api.py`: `from flask_cors import CORS` ثم `CORS(app)`،
  و `pip3 install flask-cors` في الـ Dockerfile.
- كل حاوية تعمل في طرفية مستقلة؛ لذلك نحتاج طرفيتين هنا.

```bash
# طرفية 1
docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
docker run -p 5252:5252 -it --rm softy-pinko-back-end:task3
# طرفية 2
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task3 ./front-end
docker run -p 9000:9000 -it --rm softy-pinko-front-end:task3
```
