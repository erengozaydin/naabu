# Project Discovery Naabu: Kapsamlı Rehber

## Giriş

Naabu, Project Discovery tarafından geliştirilen hızlı ve güvenilir bir port tarama aracıdır. Bu blog yazısında, Naabu'nun tüm özelliklerini, parametrelerini ve kullanım senaryolarını detaylı bir şekilde inceleyeceğiz.

## Naabu Nedir?

Naabu, Go programlama dili ile yazılmış, yüksek performanslı bir port tarama aracıdır. Hızlı ve güvenilir sonuçlar elde etmek için asenkron I/O ve özel oluşturulmuş TCP/UDP paketleri kullanır.

## Kurulum

Naabu'yu kurmak için aşağıdaki yöntemlerden birini kullanabilirsiniz:

1. Go ile kurulum:
   ```
   go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
   ```

2. GitHub'dan indirme:
   ```
   git clone https://github.com/projectdiscovery/naabu.git
   cd naabu/v2/cmd/naabu
   go build .
   mv naabu /usr/local/bin
   ```

3. Docker ile kullanım:
   ```
   docker pull projectdiscovery/naabu:latest
   ```

## Temel Kullanım

Naabu'nun en basit kullanımı şu şekildedir:

```
naabu -host example.com
```

Bu komut, example.com için varsayılan portları tarayacak ve açık olanları gösterecektir.

## Naabu Parametreleri

Naabu, çeşitli parametrelerle özelleştirilebilir. İşte en önemli parametreler ve açıklamaları:

1. `-host string`: Taranacak host veya IP adresi.
   Örnek: `naabu -host example.com`

2. `-list, -l string`: Taranacak hostların bulunduğu dosya.
   Örnek: `naabu -list hosts.txt`

3. `-port, -p string`: Taranacak portlar veya port aralıkları.
   Örnek: `naabu -host example.com -p 80,443,8000-8100`

4. `-top-ports string`: En yaygın N portu tarar.
   Örnek: `naabu -host example.com -top-ports 100`

5. `-exclude-ports, -ep string`: Taramadan hariç tutulacak portlar.
   Örnek: `naabu -host example.com -p 1-65535 -ep 22,445`

6. `-rate int`: Saniye başına paket gönderme hızı (varsayılan: 1000).
   Örnek: `naabu -host example.com -rate 500`

7. `-c int`: Eşzamanlı worker sayısı (varsayılan: 25).
   Örnek: `naabu -host example.com -c 50`

8. `-output, -o string`: Sonuçları kaydetmek için dosya adı.
   Örnek: `naabu -host example.com -o results.txt`

9. `-json`: Sonuçları JSON formatında çıktı alır.
   Örnek: `naabu -host example.com -json -o results.json`

10. `-v`: Ayrıntılı çıktı modu.
    Örnek: `naabu -host example.com -v`

## Gelişmiş Özellikler ve Parametreler

1. `-scan-all-ips`: Bir domain'in tüm IP'lerini tarar.
   Örnek: `naabu -host example.com -scan-all-ips`

2. `-interface string`: Kullanılacak ağ arayüzü.
   Örnek: `naabu -host example.com -interface eth0`

3. `-source-ip string`: Kaynak IP adresi.
   Örnek: `naabu -host example.com -source-ip 192.168.1.5`

4. `-proxy string`: SOCKS5 proxy kullanımı.
   Örnek: `naabu -host example.com -proxy socks5://127.0.0.1:9050`

5. `-nmap`: Nmap için uyumlu çıktı üretir.
   Örnek: `naabu -host example.com -nmap -o nmap_input.txt`

6. `-nmap-cli string`: Bulunan portlar için Nmap taraması çalıştırır.
   Örnek: `naabu -host example.com -nmap-cli 'nmap -sV -p'`

7. `-exclude-cdn`: CDN IP adreslerini taramadan hariç tutar.
   Örnek: `naabu -host example.com -exclude-cdn`

8. `-warm-up-time int`: Tarama öncesi bekleme süresi (saniye).
   Örnek: `naabu -host example.com -warm-up-time 10`

9. `-retries int`: Başarısız bağlantılar için yeniden deneme sayısı.
   Örnek: `naabu -host example.com -retries 3`

10. `-timeout int`: Bağlantı zaman aşımı süresi (milisaniye).
    Örnek: `naabu -host example.com -timeout 5000`

## Kullanım Senaryoları

1. Tek Bir Host için Hızlı Tarama:
   ```
   naabu -host example.com
   ```

2. Birden Fazla Host için Kapsamlı Tarama:
   ```
   naabu -list hosts.txt -p 1-65535 -c 50 -rate 1000 -o comprehensive_scan.txt
   ```

3. Belirli Portları Hariç Tutarak Tarama:
   ```
   naabu -host example.com -p 1-65535 -ep 22,3306,5432
   ```

4. En Yaygın 1000 Portu Tarama:
   ```
   naabu -host example.com -top-ports 1000
   ```

5. JSON Formatında Çıktı Alma:
   ```
   naabu -host example.com -json -o results.json
   ```

6. Nmap ile Entegre Kullanım:
   ```
   naabu -host example.com -nmap-cli 'nmap -sV -p' -o nmap_results.txt
   ```

7. CDN'leri Hariç Tutarak Tarama:
   ```
   naabu -host example.com -exclude-cdn
   ```

8. Özel Kaynak IP ve Hız Sınırlaması ile Tarama:
   ```
   naabu -host example.com -source-ip 192.168.1.5 -rate 100
   ```

## Naabu'nun Güçlü Yönleri

1. Hız: Go dilinde yazılmış olması ve asenkron I/O kullanımı sayesinde çok hızlı çalışır.
2. Özelleştirilebilirlik: Çeşitli parametrelerle farklı senaryolara uyarlanabilir.
3. Entegrasyon: Nmap gibi diğer güvenlik araçlarıyla kolayca entegre edilebilir.
4. Hassas Kontrol: Port aralıkları, hız sınırlaması, yeniden deneme sayısı gibi özelliklerle hassas kontrol sağlar.
5. CDN Farkındalığı: CDN kullanılan hedeflerde gereksiz taramaları önleyebilir.

## Sınırlamalar ve Dikkat Edilmesi Gerekenler

1. Yasal Uyarılar: Port taraması yasal sınırlamalar içerebilir, her zaman izin alınmış sistemlerde kullanın.
2. Ağ Yükü: Yüksek hızlı taramalar hedef sistemde ve ağda yük oluşturabilir.
3. Güvenlik Duvarları: Bazı güvenlik duvarları port taramalarını engelleyebilir veya yanlış sonuçlar üretebilir.
4. Yanlış Negatifler: Çok hızlı taramalar bazen açık portları kaçırabilir.

## Naabu'yu Diğer Araçlarla Birlikte Kullanma

Naabu, diğer güvenlik araçlarıyla birlikte kullanıldığında daha etkili olabilir. Örneğin:

1. httpx ile web sunucularını tespit etme:
   ```
   naabu -host example.com -p 80,443,8000-8100 | httpx
   ```

2. Nuclei ile güvenlik taraması:
   ```
   naabu -host example.com -top-ports 1000 | nuclei -t nuclei-templates/
   ```

3. Nmap ile servis versiyonu tespiti:
   ```
   naabu -host example.com -nmap-cli 'nmap -sV -p'
   ```

## Sonuç

Naabu, hızlı ve güvenilir port taraması için güçlü bir araçtır. Doğru parametrelerle kullanıldığında, güvenlik testleri, ağ keşfi ve penetrasyon testleri için çok değerli bir kaynak olabilir. Bu rehberde öğrendiklerinizle artık Naabu'yu etkili bir şekilde kullanabilir ve hedef sistemlerin açık portlarını hızlı ve verimli bir şekilde tespit edebilirsiniz.

Unutmayın, her güçlü araç gibi Naabu da sorumlu ve etik bir şekilde kullanılmalıdır. İyi taramalar!
