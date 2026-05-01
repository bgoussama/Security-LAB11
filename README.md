# 🔐 Bypass Root Detection — LAB 11

## 📸 Photo 1 — frida-ps -Uai (Setup)

<img width="1074" height="559" alt="image" src="https://github.com/user-attachments/assets/6860bc64-eb71-4b91-8e10-0a02d41030b2" />


## 📱 Application testée
UnCrackable Level 1 — OWASP MAS

---

## 📸 Photo 2 — Root detected! (Avant bypass)

<img width="476" height="1001" alt="Capture d&#39;écran 2026-04-26 210005" src="https://github.com/user-attachments/assets/6c4106be-62c3-46ad-8706-b3e5753648d2" />


---

## 🛡️ Techniques de détection bypassées

### Java
- Build.TAGS → forcé à "release-keys"
- File.exists() → false pour /system/bin/su
- Runtime.exec("su") → bloqué

### Natif
- open() → retourne -1 sur chemins suspects
- stat() → retourne -1
- access() → retourne -1

---

## 📸 Photo 3 — bypass_root.js (Bypass Java)

<img width="1107" height="220" alt="image" src="https://github.com/user-attachments/assets/481e9147-8a4c-4e20-9f3d-71277281eaad" />


---

## 📸 Photo 4 — Bypass combiné Java + Natif

<img width="1074" height="295" alt="image" src="https://github.com/user-attachments/assets/66e2d158-d23d-4972-bbe2-66e8edbac603" />


---

## 📁 Scripts créés

| Script | Rôle |
|--------|------|
| bypass_uncrackable.js | Bypass spécifique UnCrackable1 |
| bypass_root.js | Bypass Java générique |
| bypass_native.js | Bypass hooks natifs C |

---

## 📸 Photo 5 — frida-trace (Appels natifs)

<img width="843" height="693" alt="image" src="https://github.com/user-attachments/assets/6035e54e-53d2-4744-9334-4791caff4d0b" />

---

## 📸 Photo 6 — Classes root énumérées

<img width="1342" height="680" alt="image" src="https://github.com/user-attachments/assets/cf92dbec-3d1d-4a2b-8a1b-af43fa136db1" />


---

## 🔍 Résultats

Avant Frida :
→ "Root detected!" → app se ferme

Avec Frida :
→ App s'ouvre normalement ✅
→ Root non détecté ✅

<img width="422" height="756" alt="image" src="https://github.com/user-attachments/assets/42a9bca1-690f-4c21-911e-033cebd01433" />


---

## 🚀 Commandes utilisées

```bash
frida -U -f owasp.mstg.uncrackable1 \
  -l bypass_uncrackable.js \
  -l bypass_root.js \
  -l bypass_native.js

frida-trace -U -f owasp.mstg.uncrackable1 \
  -i open -i access -i stat
```

---

## ✅ Checklist
- bypass_root.js créé ✅
- bypass_native.js créé ✅
- Root detection bypassée ✅
- frida-trace exécuté ✅
- Classes root énumérées ✅
