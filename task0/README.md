# Task 0 — Create Your First Docker Image

أول صورة Docker: نبدأ من `ubuntu` الأحدث، نحدّث الحزم، ونجعل الحاوية تطبع
`Hello, World!` عند تشغيلها.

| التعليمة | وظيفتها |
| --- | --- |
| `FROM ubuntu:latest` | الصورة الأساس التي نبني فوقها |
| `RUN apt-get update` | يُنفَّذ **وقت البناء** ويصير طبقة محفوظة في الصورة |
| `RUN apt-get upgrade -y` | `-y` تتجاوز سؤال التأكيد — مهم لأن البناء غير تفاعلي |
| `CMD ["echo", "Hello, World!"]` | الأمر الافتراضي **وقت التشغيل**، لا وقت البناء |

الفرق بين `RUN` و `CMD` هو جوهر هذه المهمة: `RUN` تبني، `CMD` تشغّل.

```bash
docker build -f ./Dockerfile -t softy-pinko:task0 .
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
# Hello, World!
```
