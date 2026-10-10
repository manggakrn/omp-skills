# OMP Skills Collection

Kumpulan skill untuk Oh My Pi (OMP) - AI Coding Assistant.

## Daftar Skill

| Skill | Deskripsi |
|-------|-----------|
| `ssh` | Koneksi SSH interaktif dengan password auth via PTY |
| `deployment` | Prosedur deploy & modifikasi aman dengan analisis risiko |
| `blue-green` | Blue-green deployment dengan zero downtime |
| `server-config` | Standar konfigurasi server enterprise-grade |
| `troubleshooting` | Diagnostic tree dan root cause analysis |
| `scripting-audit` | Audit keamanan script sebelum eksekusi |
| `documentation` | Dokumentasi otomatis dengan changelog |

## Instalasi

### Opsi 1: Clone Semua Skill

```bash
# Clone repo
git clone https://github.com/manggakrn/omp-skills ~/omp-skills

# Symlink setiap skill ke folder OMP
for skill in ~/omp-skills/*/; do
  name=$(basename "$skill")
  [ -f "$skill/SKILL.md" ] && ln -sf "$skill" ~/.omp/agent/skills/"$name"
done
```

### Opsi 2: Clone Skill Tertentu Saja

```bash
git clone https://github.com/manggakrn/omp-skills ~/omp-skills

# Symlink hanya skill yang diinginkan
ln -sf ~/omp-skills/ssh ~/.omp/agent/skills/ssh
ln -sf ~/omp-skills/deployment ~/.omp/agent/skills/deployment
```

### Opsi 3: Clone Langsung ke Folder Skills

```bash
# Clone langsung (semua subfolder jadi skill)
git clone https://github.com/manggakrn/omp-skills ~/.omp/agent/skills/devops
```

## Verifikasi

Restart OMP, lalu skill akan muncul di system prompt. Model bisa membaca skill dengan:

```
skill://ssh
skill://deployment
skill://blue-green
```

## Update

```bash
cd ~/omp-skills && git pull
```

## Lisensi

MIT
