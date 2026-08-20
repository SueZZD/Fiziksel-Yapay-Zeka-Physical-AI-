
# Physical AI (Fiziksel Yapay Zeka) ve Otonom Sistem Mimarileri

<div align="center">

[![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)]()
[![Field](https://img.shields.io/badge/Field-Robotics_%26_Autonomous_Systems-blue.svg)]()
[![Author](https://img.shields.io/badge/Author-Sueda_Zeynep_Demirtas-orange.svg)]()

</div>

## 📌 İçindekiler
1. [Giriş ve Kavramsal Çerçeve](#1-giriş-ve-kavramsal-çerçeve)
2. [Temel Mimari: Algılama, Zeka ve Eylem Döngüsü](#2-temel-mimari-algılama-zeka-ve-eylem-döngüsü)
3. [İnsansı Robotlar ve Gelişmiş Donanım Entegrasyonu (Helix 02)](#3-insansı-robotlar-ve-gelişmiş-donanım-entegrasyonu-helix-02)
4. [Akıllı Şebekeler ve Dağıtık Fiziksel YZ](#4-akıllı-şebekeler-ve-dağıtık-fiziksel-yz)
5. [Modeller Evrimi: LLM, VLM ve VLA Mimarileri](#5-modeller-evrimi-llm-vlm-ve-vla-mimarileri)
6. [Uç Bilişim (Edge AI) ve Phi-4-mini-instruct Entegrasyonu](#6-uç-bilişim-edge-ai-ve-phi-4-mini-instruct-entegrasyonu)
7. [Kaynakça](#7-kaynakça)

---

## 1. Giriş ve Kavramsal Çerçeve
Fiziksel yapay zeka (Physical AI); sensör ağları, mikrodenetleyiciler ve mekanik aktüatörler vasıtasıyla fiziksel dünyayla bütünleşik ve gerçek zamanlı çalışan bir yapay zeka paradigmasıdır[cite: 2]. Ne salt yazılımdan ne de sadece donanımdan ibaret olan bu hibrit yapı; kaotik fiziksel dünyayı algılar, gürültülü verileri işleyerek deterministik çıkarımlar yapar ve bu kararları somut eylemlere dönüştürür[cite: 2].

### Geleneksel YZ vs. Fiziksel YZ
| Kriter | Geleneksel Yapay Zeka | Fiziksel Yapay Zeka |
| :--- | :--- | :--- |
| **Faaliyet Ortamı** | Sadece dijital ortamlarda bulunur (örn. LLM, veri analitiği)[cite: 2]. | Hem dijital hem de fiziksel alanlarda faaliyet gösterir[cite: 2]. |
| **Veri İşleme** | Statik/asenkron metinler, görüntüler ve dijital loglar[cite: 2]. | Gerçek dünyada dinamik sensör akışı ve fiziksel etkileşim[cite: 2]. |
| **Çıktı Formatı** | Bilgi, metin üretimi veya sanal tahminler[cite: 2]. | Tork değerleri, motor akımları ve mekanik yönlendirme komutları[cite: 2]. |
| **Otonomi** | İnsan yönlendirmesine tabidir[cite: 2]. | Gerçek zamanlı otonom karar alır[cite: 2]. |

---

## 2. Temel Mimari: Algılama, Zeka ve Eylem Döngüsü
Sistem, insan biyolojisinden ilham alan kapalı bir kontrol döngüsüne dayanır[cite: 2]:
* **Algılama (Perception):** Kameralar, LiDAR, IMU ve CAN-BUS protokolü üzerinden akan onaltılık (hexadecimal) ham log verilerinin toplanıp filtrelenmesi.
* **Zeka ve Durum Kestirimi (Intelligence):** Genişletilmiş Kalman Filtresi (EKF) ve Doğrusal Olmayan Model Öngörülü Kontrol (NMPC) algoritmalarıyla gürültülerin elimine edilerek aracın/robotun yanal durumunun kestirilmesi.
* **Eylem (Action):** Elde edilen kararların STM32 tabanlı özel veri kaydediciler veya gömülü sistemler üzerinden motor aktüatörlerine tork komutları olarak iletilmesi[cite: 2].

---

## 3. İnsansı Robotlar ve Gelişmiş Donanım Entegrasyonu (Helix 02)
Figure AI tarafından geliştirilen **Helix 02**, robotun algılama ve hareket yeteneklerini piksellerden torka dönüştüren hiyerarşik bir mimari kullanır[cite: 2]:
1. **Sistem 2 (S2 - Yavaş / Semantik Katman):** Ortamı analiz eder, dil komutlarını anlar ve üst düzey görevi planlar[cite: 2].
2. **Sistem 1 (S1 - 200 Hz Görsel-Motor Kontrol):** Kameralar ve dokunsal (tactile) sensör verilerini işleyerek eklem hedeflerini belirler[cite: 2].
3. **Sistem 0 (S0 - 1 kHz Tüm Vücut Kontrolü):** Simülasyondan gerçeğe (sim-to-real) aktarılan 10 milyon parametreli model ile yürüyüş ve denge koordinasyonunu yönetir[cite: 2].

---

## 4. Akıllı Şebekeler ve Dağıtık Fiziksel YZ
Akıllı şebekeler, "bedenlenmiş (embodied) olmayan Fiziksel Yapay Zeka" sistemlerinin en büyük örneğidir[cite: 2]. IoT donanımları ve sensör ağları aracılığıyla şebekeyi gerçek zamanlı izleyen bu sistemler; trafolara, akıllı şalterlere ve güç aktarım mekanizmalarına doğrudan müdahale ederek enerji arz-talep dengesini otonom olarak yönetir[cite: 2].

---

## 5. Modeller Evrimi: LLM, VLM ve VLA Mimarileri
* **LLM (Büyük Dil Modelleri):** Yalnızca metinsel veri işler[cite: 2].
* **VLM (Görsel-Dil Modelleri):** Kamera verisi ile metni birleştirerek çevreyi anlamlandırır[cite: 2].
* **VLA (Görsel-Dil-Eylem Modelleri):** Algılanan görsel veriyi ve komutları doğrudan donanım seviyesinde fiziksel eylemlere (direksiyon torku, frenleme) dönüştüren uçtan uca (end-to-end) sistemlerdir[cite: 2].

---

## 6. Uç Bilişim (Edge AI) ve Phi-4-mini-instruct Entegrasyonu
Saniyenin onda biri gibi kritik gecikme sürelerini tolere edemeyen otonom sistemlerde bulut bağımlılığı ortadan kaldırılmalıdır[cite: 2]. 
Araştırma kapsamında incelenen Microsoft **Phi-4-mini-instruct** modeli; 3.8 Milyar parametreli bir SLM (Small Language Model) olmasına karşın sunduğu **128k token bağlam uzunluğu (context window)** sayesinde[cite: 2]; CAN-BUS log ağlarının incelenmesi, ROS 2 düğümlerinin analizi ve gömülü sistem optimizasyonlarında donanım sınırlarını zorlamadan bütüncül analiz imkanı tanır[cite: 2].

---

## 7. Kaynakça
*(Tam kaynakça listesi raporun orijinal dokümanında [1-30] aralığında detaylandırılmıştır.)*
