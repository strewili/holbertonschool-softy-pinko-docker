# Task 1 — Back-end

نضيف Python و pip و Flask إلى الصورة، ونشغّل سيرفر API صغير بنقطة نهاية
واحدة `/api/hello`.

## نقاط مهمة

- **`host='0.0.0.0'` وليس `127.0.0.1`** — داخل الحاوية، `127.0.0.1` يعني
  الحاوية نفسها فقط، فلن يصلك شيء من خارجها. `0.0.0.0` تعني "استمع على كل
  الواجهات".
- **Flask يُثبَّت بـ `pip3` لا بـ `apt-get`** حسب متطلبات المشروع.
- **`rm /usr/lib/python*/EXTERNALLY-MANAGED`** — توزيعات Ubuntu الحديثة تمنع
  pip من التثبيت على مستوى النظام؛ هذا السطر يرفع المنع داخل الحاوية.
- **`-p 5252:5252`** — بدون ربط المنفذ، السيرفر يعمل لكن لا أحد يصله.

```bash
docker build -f ./Dockerfile -t softy-pinko:task1 .
docker run -p 5252:5252 -it --rm --name softy-pinko-task1 softy-pinko:task1
curl http://localhost:5252/api/hello
```
