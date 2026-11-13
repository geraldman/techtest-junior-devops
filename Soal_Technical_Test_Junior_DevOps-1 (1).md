# Tugas Docker

## Tujuan
Menguji kemampuan dasar containerization dan security setup melalui studi kasus deployment WordPress.

## Studi Kasus
Deploy aplikasi **WordPress** dengan **PostgreSQL** sebagai database, di belakang **Nginx** sebagai reverse proxy, menggunakan Docker.

---

## 1. Docker & Docker Compose

**Buat Dockerfile sendiri** (bukan pakai image jadi dari Docker Hub) untuk 3 service:
- WordPress
- PostgreSQL
- Nginx (reverse proxy)

> Base image bebas (misal `alpine`, `debian-slim`, dll), sesuaikan dengan kebutuhan masing-masing service.

**Ketentuan wajib:**
| No | Ketentuan | Detail |
|----|-----------|--------|
| 1 | Isolasi network | DB **hanya** boleh diakses oleh WordPress. Nginx dan luar tidak boleh akses DB langsung. Gunakan minimal 2 Docker network (misal: `frontend` dan `backend`). |
| 2 | Non-root user | Semua container wajib jalan dengan user non-root, **UID ≥ 10000**. |
| 3 | Healthcheck | Setiap container wajib punya `HEALTHCHECK` (di Dockerfile atau docker-compose). |
| 4 | Build | `docker-compose.yml` wajib pakai `build:` (bukan `image:`) untuk ketiga service. |

**Struktur network yang diharapkan:**
```
Internet → Nginx (frontend network) → WordPress (frontend + backend network) → PostgreSQL (backend network only)
```

---

## 2. HTTPS & Domain

- Akses aplikasi wajib via **domain name** (boleh domain lokal/`/etc/hosts`, tidak wajib domain publik).
- Traffic wajib **HTTPS** (self-signed certificate diperbolehkan).
- Konfigurasi SSL dilakukan di sisi **Nginx**.

---


## Checklist Deliverables

Gunakan checklist ini untuk memastikan submission sudah lengkap sebelum dikirim:

- [ ] Dockerfile WordPress (custom, non-root UID ≥ 10000, healthcheck)
- [ ] Dockerfile PostgreSQL (custom, non-root UID ≥ 10000, healthcheck)
- [ ] Dockerfile Nginx (custom, non-root UID ≥ 10000, healthcheck)
- [ ] `docker-compose.yml` menggunakan `build:` untuk semua service
- [ ] Network terisolasi — DB tidak bisa diakses langsung dari luar/Nginx
- [ ] Akses aplikasi via domain name
- [ ] HTTPS aktif (certificate, meskipun self-signed)
- [ ] README.md (arsitektur, cara menjalankan, opsional screenshot)
- [ ] Source code sudah di-push ke GitHub repository
- [ ] *(Bonus)* mTLS antara Nginx dan client/antar service
- [ ] *(Bonus)* GitHub Actions — build & push image ke Docker Hub

---

## Bonus (Nilai Tambah)

| Bonus | Deskripsi |
|-------|-----------|
| mTLS | Tambahkan mutual TLS (client certificate) antara Nginx dan client, atau antar service. |
| CI/CD | Buat GitHub Actions workflow yang otomatis build image dan push ke Docker Hub setiap ada push ke branch tertentu. |

---

## Kriteria Penilaian

1. **Kebenaran fungsional** — aplikasi WordPress berjalan dan bisa diakses via HTTPS.
2. **Keamanan** — isolasi network, non-root user, HTTPS berjalan sesuai ketentuan.
3. **Kualitas kode** — struktur project rapi, Dockerfile efisien
4. **Dokumentasi** — README jelas dan mudah diikuti.
5. **Bonus**  (nilai tambah, bukan wajib).

## Estimasi Waktu
2 hari kerja.
