# ATS - Applicant Tracking System

Üniversite bitirme projesi olarak geliştirilen, stajyer başvuru süreçlerini yöneten full-stack web uygulaması.

## Özellikler

**Aday (User) Tarafı:**
- Kayıt, e-posta doğrulama, şifre sıfırlama
- Profil ve CV yönetimi
- Açık pozisyonlara başvuru
- Görev takibi ve dosya yükleme
- Müsaitlik takvimi

**Admin Tarafı:**
- İlan oluşturma ve yönetimi
- Başvuru değerlendirme ve durum takibi
- Görev atama, timeline ve proje takibi
- Toplu e-posta gönderimi
- CSV export, admin notları
- Soru havuzu yönetimi

## Teknolojiler

| Katman | Teknoloji |
|--------|-----------|
| Backend | Java 17, Spring Boot 3.3, Spring Security, JWT |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS |
| Veritabanı | PostgreSQL 16, Flyway (migration) |
| Containerization | Docker, Docker Compose |
| E-posta | Spring Mail + Mailpit (dev) |

## Proje Yapısı

```
├── backend/                # Spring Boot API
│   ├── src/main/java/      # Java kaynak kodları
│   │   └── com/project/project/
│   │       ├── config/     # Konfigürasyon ve exception handler
│   │       ├── controller/ # REST controller'lar
│   │       ├── dto/        # Request/Response DTO'lar
│   │       ├── entity/     # JPA entity'ler
│   │       ├── repository/ # Spring Data JPA repository'ler
│   │       ├── security/   # JWT, authentication
│   │       └── service/    # İş mantığı
│   ├── src/main/resources/
│   │   └── db/migration/   # Flyway SQL migration'ları
│   └── Dockerfile
├── frontend/               # React SPA
│   ├── src/
│   │   ├── api/            # Axios API client
│   │   ├── auth/           # Auth context ve hooks
│   │   ├── components/     # UI bileşenleri
│   │   ├── pages/          # Sayfa bileşenleri
│   │   ├── hooks/          # Custom hooks
│   │   ├── lib/            # Utility fonksiyonları
│   │   └── theme/          # Tema yönetimi
│   └── Dockerfile
├── scripts/                # Yardımcı scriptler
├── docker-compose.yml      # Tüm servisleri ayağa kaldırır
└── .env.example            # Ortam değişkenleri şablonu
```

## Kurulum

### Gereksinimler

- [Docker](https://docs.docker.com/get-docker/) ve Docker Compose
- Git

### Hızlı Başlangıç

1. **Projeyi klonlayın:**
   ```bash
   git clone https://github.com/<kullanici-adi>/ats.git
   cd ats
   ```

2. **Ortam değişkenlerini hazırlayın:**
   ```bash
   cp .env.example .env
   ```

3. **Konteynerleri başlatın:**
   ```bash
   docker compose up -d --build
   ```

4. **Uygulamaya erişin:**

   | Servis | Adres |
   |--------|-------|
   | Frontend | http://localhost:3000 |
   | Backend API | http://localhost:8080/api/v1 |
   | Mailpit (SMTP UI) | http://localhost:8025 |

### Varsayılan Admin Hesabı

Uygulama ilk başlatıldığında veritabanında admin yoksa otomatik olarak oluşturulur:

- **E-posta:** `admin@32bit.com.tr`
- **Şifre:** `Admin12345!`

Bu bilgiler `.env` dosyasından değiştirilebilir.

### Lokal Geliştirme (Docker olmadan)

**Backend:**
```bash
cd backend
./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev
```

> Not: Lokal geliştirme için PostgreSQL ve Mailpit ayrıca çalışıyor olmalıdır.

## Veritabanı Sıfırlama

```bash
docker compose down -v
docker compose up -d --build
```

Veya yardımcı script ile:

```bash
# Linux / macOS
bash ./scripts/reset-db.sh

# Windows (PowerShell)
.\scripts\reset-db.ps1
```

## API Mimarisi

- RESTful API, `/api/v1` prefix'i altında
- JWT tabanlı kimlik doğrulama (Bearer token)
- Role-based access control: `USER`, `ADMIN`
- Flyway ile otomatik veritabanı migration
- Dosya yükleme (CV, görev ekleri) - max 50MB

## Lisans

Bu proje bir üniversite bitirme projesidir.
