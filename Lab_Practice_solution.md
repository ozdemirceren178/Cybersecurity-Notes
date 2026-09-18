# Telnet

Telnet, uzak bir bilgisayara terminal üzerinden bağlanmayı sağlayan bir protokoldür. Ancak bağlantı şifrelenmediği için güvenli değildir. Günümüzde uzak bağlantı için genellikle **SSH** tercih edilir.

**Varsayılan port:** TCP 23

## Labda ne yaptım?

Bu labda hedef makinede çalışan **Telnet servisini bulup bağlantı kurmam** ve bağlantıdan sonra makine hakkında bazı bilgileri öğrenmem istendi.

### 1. Açık portu buldum

Öncelikle hedef makinede hangi portların açık olduğunu görmek için Nmap kullandım:

```bash
nmap <hedef-ip>
```

Tarama sonucunda **TCP 23 portunun açık** olduğunu gördüm.

→ TCP 23 açık olduğuna göre Telnet servisi olabileceğini düşündüm.

### 2. Telnet servisine bağlandım

Açık olan 23 numaralı porta Telnet ile bağlandım:

```bash
telnet <hedef-ip> 23
```

Bağlantı ekranı geldikten sonra labda verilen kullanıcı adı ve şifre ile giriş yaptım.

### 3. Hostname bilgisini buldum

Bağlantı kurduktan sonra hangi makinede olduğumu görmek için:

```bash
hostname
```

komutunu kullandım.

### 4. Çalışma dizinini buldum

Bağlandıktan sonra hangi dizinde bulunduğumu öğrenmek için:

```bash
pwd
```

komutunu kullandım.

## Labı nasıl çözdüm?

**Nmap → 23/TCP açık → Telnet olduğunu tespit ettim → Telnet ile bağlandım → giriş yaptım → `hostname` ve `pwd` ile istenen bilgileri buldum.**

## Bu labdan aklımda kalanlar

* Telnet → **TCP 23**
* Telnet bağlantısı **şifreli değildir**.
* `nmap` → açık portları/servisleri keşfetmek için.
* `telnet <IP> 23` → Telnet servisine bağlanmak için.
* `hostname` → makinenin adını gösterir.
* `pwd` → mevcut çalışma dizinini gösterir.
* Güvenli uzak bağlantı için **SSH** tercih edilir.
