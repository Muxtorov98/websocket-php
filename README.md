# WebSocket PHP Server

Bu loyiha WebSocket PHP serverini Docker yordamida oson va tez ishga tushirish uchun mo'ljallangan. Docker Compose fayli orqali konteynerlarni boshqarish mumkin.

## Loyihaning tavsifi

- **Xizmat nomi:** `websocket-php`
- **Konteyner nomi:** `websocket`
- **Portlar:** 8080 portidan tashqi va ichki portga bog'lanadi
- **Qurilish:** Dockerfile yordamida `./socket` katalogidan quriladi

## Qanday ishlatish

### 1. Zarur dasturlarni o'rnatish

- Docker
- Docker Compose

**Tekshirish:**

```bash
docker --version
docker compose --version
```

Agar o'rnatilmagan bo'lsa, [Docker rasmiy sayti](https://docs.docker.com/get-docker/) orqali o'rnatishingiz mumkin.

### 2. Loyihangiz katalogiga o'ting

```bash
cd /path/to/your/project
```

*`/path/to/your/project`* o'rniga sizning loyihangiz joylashgan katalogni kiriting.

### 3. Docker Compose yordamida konteynerlarni ishga tushurish

```bash
docker compose up -d
```

Bu buyruq konteynerlarni fon rejimida ishga tushiradi.

### 4. Ishga tushgan konteynerlarni tekshirish

```bash
docker ps
```

Bu buyruq sizga ishga tushgan konteynerlar ro'yxatini ko'rsatadi. Sizda quyidagicha bo'lishi kerak:

```
CONTAINER ID   IMAGE             COMMAND       CREATED       STATUS       PORTS                  NAMES
<id>           websocket-php     "docker-entr..."   <time>   Up <time>   0.0.0.0:8080->8080/tcp   websocket
```

### 5. Test qilish uchun WebSocket mijoz bilan ulanish

Server 8080 portida ishlamoqda. Siz WebSocket mijoz yordamida unga ulanishni sinab ko'rishingiz mumkin.

#### Misol uchun, Chrome DevTools yoki Browser WebSocket test vositasi:

- URL: `ws://localhost:8080`

Agar sizda WebSocket serveringiz to'g'ri ishlayotgan bo'lsa, u bilan ulanish va xabar yuborish mumkin bo'ladi.

### 6. WebSocket serverini test qilish uchun JavaScript misol

Quyidagi kodni browser konsoliga yozib, ulanish va xabar yuborishni sinab ko'ring:

```js
const ws = new WebSocket('ws://localhost:8080');

ws.onopen = () => {
  console.log('Ulandi');
  ws.send('Salom, WebSocket!');
};

ws.onmessage = (event) => {
  console.log('Qabul qilingan xabar:', event.data);
};

ws.onerror = (error) => {
  console.error('Xatolik:', error);
};

ws.onclose = () => {
  console.log('Ulanish yopildi');
};
```

### 7. Konteynerlarni to'xtatish

```bash
docker compose down
```

Bu buyruq barcha konteynerlarni to'xtatadi va o'chiradi.

## Qo'shimcha ma'lumotlar

- `docker compose.yml` fayli `./socket` katalogidan Dockerfile yordamida konteynerni quradi.
- Server 8080 portida ishlaydi; uni o'zgartirish uchun `docke compose.yml` faylini tahrirlashingiz mumkin.
