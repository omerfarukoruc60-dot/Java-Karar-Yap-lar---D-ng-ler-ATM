[RAPOR.md](https://github.com/user-attachments/files/35287008/RAPOR.md)
# ATM Simülasyonu Raporu

## 1. Programın Amacı
Bu program, bir bankanın ATM sistemini konsol üzerinde simüle eder. Kullanıcı çıkış yapana kadar çalışan bir menü sunar; bakiye görüntüleme, para yatırma ve para çekme işlemlerini yapar, ayrıca işlem sayısını ve toplam tutarları takip eder.

## 2. Kullanılan Değişkenler
| Değişken | Tür | Açıklama |
|---|---|---|
| `bakiye` | int | Hesaptaki para. Başlangıç değeri 10000 TL |
| `islemSayisi` | int | Başarılı yatırma ve çekme işlemlerinin sayısı |
| `toplamYatirilan` | int | Başarılı yatırma işlemlerinin toplam tutarı |
| `toplamCekilen` | int | Başarılı çekme işlemlerinin toplam tutarı |
| `kullaniciSecim` | int | Kullanıcının menüden seçtiği numara |
| `kullaniciYatirma` / `kullaniciCekme` | int | Yatırılmak veya çekilmek istenen tutar |

## 3. Programın Çalışma Mantığı
1. Program başlarken `bakiye` 10000 TL, sayaçlar 0 olarak ayarlanır ve karşılama mesajı yazılır.
2. `while (true)` döngüsü ile menü sürekli gösterilir. Her işlemden sonra menü yeniden görünür.
3. Kullanıcının seçimine göre `if - else if` yapısı ile ilgili işlem yapılır:
   - **1:** Bakiye yazdırılır.
   - **2:** Tutar sorulur. Tutar 0 veya negatifse işlem yapılmaz ve hata mesajı verilir. Aksi halde bakiyeye eklenir, `toplamYatirilan` ve `islemSayisi` güncellenir.
   - **3:** Tutar sorulur. Tutar 0 veya negatifse ya da bakiyeden büyükse işlem yapılmaz. Aksi halde bakiyeden düşülür, `toplamCekilen` ve `islemSayisi` güncellenir.
   - **4:** Toplam işlem sayısı ile toplam yatırılan ve çekilen tutar gösterilir.
   - **0:** `break` ile döngüden çıkılır.
   - **Diğer:** "Gecersiz sayi, basa donuyorsunuz." mesajı gösterilir.
4. Döngüden çıkınca son bakiye ve toplam işlem sayısı yazdırılır, program sonlanır.

## 4. Akış Şeması
![Akış şeması](docs/akis-semasi.png)

## 5. Gereksinimlerin Karşılanması
| Gereksinim | Durum |
|---|---|
| Başlangıç bakiyesi 10.000 TL | Karşılandı |
| Menü: bakiye, yatırma, çekme | Karşılandı (çıkış için 0 kullanılıyor) |
| Sürekli çalışan menü, çıkışa kadar devam | Karşılandı (`while (true)`) |
| Sıfır veya negatif yatırma kabul edilmez | Karşılandı (`<= 0` kontrolü) |
| Çekmede bakiye kontrolü, yetersizse işlem yok | Karşılandı |
| Geçersiz menü seçiminde hata mesajı | Karşılandı |
| Her işlemden sonra menü tekrar gösterilir | Karşılandı |
| Çıkışta program sonlanır | Karşılandı |
| Toplam işlem sayısını görme | Karşılandı (menü 4) |
| Başarılı yatırma ve çekme toplamları | Karşılandı |
| Kapanmadan önce son bakiye ve işlem sayısı | Karşılandı |

## 6. Test Senaryoları
| Girdi | Beklenen sonuç | Sonuç |
|---|---|---|
| Menü 1 | 10000 TL bakiye gösterilir | Doğru |
| Yatırma: 500 | Bakiye 10500 olur, işlem sayısı 1 | Doğru |
| Yatırma: 0 veya -50 | Hata mesajı, bakiye değişmez | Doğru |
| Çekme: 200 | Bakiye düşer, işlem sayısı artar | Doğru |
| Çekme: bakiyeden büyük tutar | "Bakiyeniz yetersiz.", bakiye değişmez | Doğru |
| Menü 9 | Geçersiz seçim mesajı | Doğru |
| Menü 4 | İşlem sayısı ve toplamlar gösterilir | Doğru |
| Menü 0 | Son bakiye ve işlem sayısı yazılır, program kapanır | Doğru |

## 7. Karşılaşılan Sorunlar ve Notlar
- Sıfır tutar başlangıçta kabul ediliyordu; kontrol `< 0` yerine `<= 0` yapılarak düzeltildi.
- Kullanıcı sayı yerine harf girerse `nextInt()` hata verir. Bu durum ödev kapsamında ele alınmamıştır, geliştirilebilir.
- Başarısız işlemler (hatalı tutar, yetersiz bakiye) işlem sayısına eklenmemiştir.
