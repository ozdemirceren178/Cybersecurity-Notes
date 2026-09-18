# Nmap — Ağ Tarama

**Nmap (Network Mapper)**, ağdaki cihazları keşfetmek, açık portları görmek ve çalışan servisler hakkında bilgi toplamak için kullanılan bir ağ tarama aracıdır.

> ⚠️ Nmap yalnızca kendi sistemlerimde, lab ortamlarında veya izin verilen hedeflerde kullanılmalıdır.

---

## 1. Host Keşfi

Öncelikle ağda **hangi cihazların aktif olduğunu** bulmak için kullanılır. Portları tek tek taramak yerine aktif hostları keşfetmeye odaklanır.

```bash
nmap -sn 192.168.1.0/24
```

Buradaki `-sn`, **port taraması yapmadan host keşfi** yapılmasını sağlar.

---

## 2. TCP SYN Scan

Bir sistemdeki **TCP portlarının açık olup olmadığını** kontrol etmek için kullanılır.

```bash
nmap -sS 192.168.1.10
```

`-sS`, SYN paketleri kullanarak tarama yapar. Genellikle hızlı ve yaygın kullanılan Nmap tarama yöntemlerinden biridir.

**Kısaca:** TCP portlarını kontrol etmek → `-sS`

---

## 3. TCP Connect Scan

TCP bağlantısını normal işletim sistemi bağlantı mekanizmasıyla kurarak portu kontrol eder.

```bash
nmap -sT 192.168.1.10
```

SYN scan kullanılamadığında veya normal TCP bağlantısı üzerinden tarama yapmak gerektiğinde kullanılabilir.

**Kısaca:** Normal TCP bağlantısıyla port tarama → `-sT`

---

## 4. UDP Scan

TCP yerine **UDP kullanan servisleri** keşfetmek için kullanılır.

```bash
nmap -sU 192.168.1.10
```

Örneğin DNS gibi UDP kullanan servisleri kontrol etmek için kullanılabilir.

UDP taramaları TCP taramalarına göre daha yavaş olabilir.

**Kısaca:** UDP portlarını kontrol etmek → `-sU`

---

## 5. FIN, NULL ve Xmas Scan

Bunlar TCP flag'lerinin farklı şekilde kullanıldığı özel tarama teknikleridir.

### FIN Scan

```bash
nmap -sF 192.168.1.10
```

FIN flag'i kullanılarak portların durumu hakkında bilgi edinmeye çalışır.

### NULL Scan

```bash
nmap -sN 192.168.1.10
```

TCP flag'leri ayarlanmadan tarama yapılır.

### Xmas Scan

```bash
nmap -sX 192.168.1.10
```

Birden fazla TCP flag'i kullanılır.

🧠 **Bunların amacı:** TCP'nin farklı davranışlarından yararlanarak port durumu hakkında bilgi toplamaktır.

---

## 6. ACK Scan

Firewall veya paket filtreleme kurallarını anlamaya yardımcı olmak için kullanılır.

```bash
nmap -sA 192.168.1.10
```

Burada asıl amaç doğrudan "port açık mı?" demekten çok, **portların filtrelenip filtrelenmediğini** anlamaktır.

**Kısaca:** Firewall/filtreleme hakkında bilgi → `-sA`

---

## 7. Idle Scan

Taramanın kaynağını gizlemeye yönelik ileri düzey bir tekniktir. Başka bir hostun ("zombie host") ağ davranışından yararlanır.

```bash
nmap -sI <zombie-host> <hedef>
```

Normal Nmap taramalarına göre daha ileri düzey bir tekniktir ve özel koşullar gerektirir.

---

# 8. Servis ve Versiyon Tespiti

Açık bir portun arkasında **hangi servis ve sürümün çalıştığını** öğrenmek için kullanılır.

```bash
nmap -sV 192.168.1.10
```

Örneğin sonuçta:

```text
22/tcp  open  ssh
80/tcp  open  http
```

gibi bilgiler görülebilir.

`-sV` → **Service Version Detection**

---

# 9. İşletim Sistemi Tespiti

Hedef sistemin hangi işletim sistemini kullandığı hakkında tahmin yapmak için kullanılır.

```bash
nmap -O 192.168.1.10
```

Nmap bunu ağ davranışlarına bakarak tahmin eder. Bu nedenle sonuç her zaman kesin olmayabilir.

`-O` → **OS Detection**

---

# 10. Timing

Nmap taramasının hızını ayarlamak için kullanılır.

```bash
nmap -T4 192.168.1.10
```

Örneğin:

* `-T0` → Çok yavaş
* `-T1` → Yavaş
* `-T2` → Daha yavaş
* `-T3` → Varsayılan
* `-T4` → Hızlı
* `-T5` → Çok hızlı/agresif

Günlük kullanımda `-T4` ile sık karşılaşabilirim.

---

# 11. NSE — Nmap Scripting Engine

Nmap'in script sistemi sayesinde standart taramaların ötesinde çeşitli kontroller yapılabilir.

Örneğin:

```bash
nmap --script <script-adı> 192.168.1.10
```

NSE scriptleri servis keşfi, bilgi toplama ve çeşitli güvenlik kontrollerinde kullanılabilir.

---

