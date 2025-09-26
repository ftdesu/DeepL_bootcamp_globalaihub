#  Architectural Heritage Elements Classification  

 Bu proje, **Akbank Derin Öğrenme Bootcamp 2025** kapsamında geliştirilmiştir.  

Amaç, **CNN tabanlı derin öğrenme mimarileri ve transfer öğrenme yöntemleri** kullanarak mimari miras öğelerinin (sunak, apsis, kubbe, uçan payanda, vitray vb.) görseller üzerinden sınıflandırılmasıdır.  

---

##  Dataset  
- **Kaynak:** Kaggle → *Architectural Heritage Elements Image64*  
- **Sınıf sayısı:** 10  
- **Görsel sayısı:** ~10,235  
- Veri eğitim / doğrulama / test setlerine ayrılmıştır.  
- Görseller farklı çözünürlüklerde hazırlanmıştır: `64x64` ve `128x128`.  

**Sınıflar:**  
`sunak, apsis, çan kulesi, sütun, kubbe (iç), kubbe (dış), uçan payanda, yalungöz, vitray, tonoz`

---

##  Yol Haritası  

0. Gerekli Kütüphaneler  
1. Veri Keşif (EDA)  
2. Veri Hazırlık (64x64)  
3. Temel CNN Modeli (64x64)  
4. Model Derleme ve Eğitim  
5. Model Değerlendirme  
6. VGG16 Transfer Öğrenme (64x64)  
7. VGG16 Transfer Öğrenme (128x128)  
8. VGG16 Fine-Tuning (128x128)  
9. Sonuç Karşılaştırma  
10. Grad-CAM Açıklanabilirlik  
11. Genel Değerlendirme  

---

##  Modeller ve Sonuçlar  

| Model                        | Input Size | Strateji             | En İyi Val Acc | Test Acc |
|------------------------------|------------|----------------------|----------------|----------|
| **Temel CNN**                | 64x64      | Sıfırdan eğitim      | **81.5%**      | 70.7%    |
| **VGG16 (Frozen)**           | 64x64      | Transfer             | 81.4%          | -        |
| **VGG16 (Frozen)**           | 128x128    | Transfer             | 81.0%          | -        |
| **VGG16 (Fine-Tuning)**     | 128x128    | Son blok açıldı      | **92.1%**      | **91.7%** |

---

##  Grad-CAM Açıklanabilirlik  

Modelin odaklandığı bölgeler **Grad-CAM ısı haritaları** ile incelenmiştir:  
- **Doğru tahminlerde** → Model mimari öğelerin **ayrıştırıcı bölgelerine** odaklandı:  
  - *Vitray* → cam yüzeyi & renk kontrastı  
  - *Kubbe(Dış)* → kubbenin yuvarlak silueti  
  - *Sunak* → merkezdeki ikonografik detay  

- **Yanlış tahminlerde** → Benzer yapılar çakıştı:  
  - *Uçan Payanda ↔ Kubbe(Dış)* → dış kemer & gökyüzü görsellerinde yanlış odaklanmalar  

Sonuç: Model sadece ezberlemiyor, insan uzmanların da dikkate aldığı bölgelere yoğunlaşıyor → **yorumlanabilir yapay zeka (XAI)** desteği sağlandı.
---


##  Genel Değerlendirme  

- **En iyi performans**: `VGG16 Fine-Tuning (128x128)` → %91.7 test doğruluğu  
- **Kolay sınıflar**: Vitray, Tonoz, Kubbe(Dış)  
- **Zorlayıcı sınıflar**: Apsis (az veri) ve Uçan Payanda (benzerlik nedeniyle karışıklık)  
- **Grad-CAM** → modelin karar süreçlerini açıklanabilir hale getirdi.  

Sonuç olarak proje, **yüksek doğruluk** ve **açıklanabilir yapay zeka** birleşimiyle başarılı bir mimari miras sınıflandırma sistemi ortaya koymaktadır.  

---
##  Kaggle Notebook
https://www.kaggle.com/code/ftdesu/deepl-bootcamp-globalaihub-ft
##  Kullanım  
Notebook içerisinde:  
- `3. Temel CNN Modeli`  
- `6. VGG16 Transfer (64x64)`  
- `7. VGG16 Transfer (128x128)`  
- `8. VGG16 Fine-Tuning`  
- `10. Grad-CAM Açıklanabilirlik`  
- `11. Genel Değerlendirme`  

adımlarını izleyerek çalışma süreci takip edilebilir.  

---

