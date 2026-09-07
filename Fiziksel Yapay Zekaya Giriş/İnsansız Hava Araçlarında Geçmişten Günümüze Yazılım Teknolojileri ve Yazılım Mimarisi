# İnsansız Hava Araçlarında Geçmişten Günümüze Yazılım Teknolojileri ve Yazılım Mimarisi

<div align="center">

[![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)]()
[![Field](https://img.shields.io/badge/Field-UAVs_%26_Reasoning_VLA-blue.svg)]()
[![Author](https://img.shields.io/badge/Author-Sueda_Zeynep_Demirtas-orange.svg)]()

</div>

## 📌 İçindekiler
1. [Giriş: Klasik Otonomiden Yapay Zeka Odaklı Yaklaşımlara](#1-giriş-klasik-otonomiden-yapay-zeka-odaklı-yaklaşımlara)
2. [VLA (Vision-Language-Action) Mimarileri ve Çalışma Prensibi](#2-vla-vision-language-action-mimarileri-ve-çalışma-prensibi)
3. [Akıl Yürütme Tabanlı VLA (Reasoning-VLA) ve Embodied CoT](#3-akıl-yürütme-tabanlı-vla-reasoning-vla-ve-embodied-cot)
4. [İnsansız Hava Araçlarında (UAV) VLA ve Öğrenilmiş Kontrol Sistemleri](#4-insansız-hava-araçlarında-uav-vla-ve-öğrenilmiş-kontrol-sistemleri)
5. [Kaynakça](#5-kaynakça)

---

## 1. Giriş: Klasik Otonomiden Yapay Zeka Odaklı Yaklaşımlara
Geçmişten günümüze insansız hava araçlarında (İHA) kullanılan yazılım mimarilerinden ilki; algılama (perception), eş zamanlı konum belirleme ve haritalama (SLAM) ve kontrol şeklinde 3 ayrı katmana bölünmüş klasik otonom yaklaşımıdır. 

* **Perception Katmanı:** Sensörler aracılığıyla çevreyi algılar ve ham veriyi işleyerek kullanılabilir hale getirir. Örneğin, LiDAR sensöründen gelen ham nokta bulutlarının (point cloud) kümelenmesi (clustering) ve nesnelerin anlamlandırılması bu katmanda yer alır. Derin öğrenmeye dayalı görüntü işleme ve bilgisayarlı görü teknolojilerinin yer aldığı, yapay zekanın otonom sistemlere dahil olduğu ilk katmandır.
* **Kontrol Katmanı:** Üst düzey otonomi yazılımı ile fiziksel donanım arasındaki köprü görevini üstlenerek aracın dinamik hareketlerini yönetir. Kontrol katmanının başarısı doğrudan SLAM katmanına bağlıdır; konumu yeterli doğrulukla tespit edilemeyen bir cihazı kontrol etmek mümkün değildir. SLAM katmanının durum kestirimi (state estimation) ve EKF (Genişletilmiş Kalman Filtresi) gibi algoritmalarla elde ettiği bilgiler üzerine kurulan kontrol katmanı; pure pursuit, PID, MPC ve NMPC gibi ağır matematiksel algoritmalarla cihazı yönetir.

<img width="600" alt="Klasik Otonom Mimarisi" src="https://github.com/user-attachments/assets/cls-arch-placeholder" />

Klasik otonomiden bu yana yaşanan en büyük değişim, önce sadece perception katmanına yapay zekanın dahil olması, ardından ise ara katmanların da yapay zekayla donatılmasıdır. Savunma sanayisi gibi kritik alanlarda en ufak bir halüsinasyon veya model hatası küresel sorunlara yol açabileceğinden "sağlam matematik" ve klasik yöntemler ağırlığını korusa da; birçok alanda yapay zeka otonomi mutfağının vazgeçilmezi haline gelmiştir.

---

## 2. VLA (Vision-Language-Action) Mimarileri ve Çalışma Prensibi
Görsel veriyi ve doğal dili işleyip doğrudan eyleme dönüştüren **VLA (Vision-Language-Action)** mimarisi, fiziksel donanıma doğrudan temas etmesi ve dinamik karar mekanizmaları sunması nedeniyle modern otonomi sistemlerinin merkezinde yer alır.

* **VLA Tanımı:** Görsel algıyı, dil anlama yeteneğini ve eyleme geçmeyi birleştiren bir yapay zeka modelidir[cite: 1].
* Bu yapılar, üst seviye görsel-dilsel muhakeme yeteneğini hassas eylem yörüngelerine dönüştürerek hareket planlama ve kontrol süreçlerine esneklik kazandırır[cite: 2].

<img width="700" alt="COMPASS Mimari ve Katmanlar" src="https://github.com/user-attachments/assets/vla-arch-placeholder" />

VLA'lerin otonom sistemlerde yaygınlaşması; çok adımlı çıkarım süreçlerinin gerçek zamanlı yüksek frekanslı kontrolü kısıtlaması, farklı araç ve senaryolara genelleme yapabilecek geniş ölçekli veri eksikliği gibi etkenler nedeniyle **Reasoning VLA (Akıl Yürütme Temelli VLA)** modellerinin doğmasına yol açmıştır[cite: 3].

---

## 3. Akıl Yürütme Tabanlı VLA (Reasoning-VLA) ve Embodied CoT
Reasoning VLA; görsel algıyı, dil anlama yeteneğini ve eylem planlamayı adım adım akıl yürütmeyle bütünleştiren birleşik bir yapay zeka modelidir[cite: 1, 3]. OpenAI o1/o3 veya DeepSeek-R1 gibi modellerde görülen Chain-of-Thought (Düşünce Zinciri) mantığını fiziksel dünyaya uyarlayan **Embodied CoT (Fizikselleştirilmiş Akıl Yürütme)** mimarisine dayanır.

### Çift Katmanlı (Dual-Model) Hiyerarşik Mimari
* **Bilişsel Katman (Cognitive Core / Slow Thinking):** Üst düzey planlama, tehlike (hazard) analizi, semantik çıkarım ve rota optimizasyonunu yönetir. Görevi analiz edip eyleme geçmeden önce kendi içinde bir düşünce zinciri kurar.
* **Reaktif Katman (Control Core / Fast Thinking):** Bilişsel katmandan gelen komutları alır, anlık olarak 4D uçuş koordinatlarına veya motor torkuna dönüştürür.

### COMPASS Referans Mimarisi
Akıllı şehirler veya karmaşık lojistik ağlarındaki drone'lar için geliştirilen **COMPASS** gibi 7 katmanlı teknik referans mimarileri, akıl yürütmeyi bir **"Semantik Ara Katman" (Semantic Middleware Layer)** olarak konumlandırır[cite: 1]. Bu katman, doğal dil komutunu yasal havacılık regülasyonları ve batarya kısıtlarıyla çarpıştırarak arka planda semantik akıl yürütme gerçekleştirir[cite: 1].

### Geleneksel İHA vs. Agentic (Akıl Yürüten) İHA Karşılaştırması

| Boyut / Kriter | Geleneksel İHA'lar | Agentic İHA'lar |
| :--- | :--- | :--- |
| **Algı Modalitesi** | Monoküler/stereo RGB, temel multispektral/termal kameralar; sınırlı anlamsal çözümleme. | Çok modlu algılama (RGB, termal, LiDAR, hiperspektral); VLM destekli anlamsal zeminleme (semantic grounding). |
| **Kontrol Mimarisi** | Kural tabanlı uçuş kontrolcüleri, waypoint takip eden otopilotlar. | Algı, planlama, bellek ve öz-değerlendirmeyi birleştiren katmanlı ajan kontrol döngüleri. |
| **Karar Sistemi** | Çıkarım yeteneği olmayan deterministik, scripted mantık. | Pekiştirmeli öğrenme tabanlı karar motorları, hafıza destekli modüller, imkân farkındalıklı akıl yürütme. |
| **Otonomi Seviyesi** | Seviye 1–2 (Temel otonomi; döngüde insan operatör zorunludur). | Seviye 4–5 (Bağlam farkındalıklı otonomi; asgari insan denetimi). |
| **Görev Uyarlanabilirliği** | Statik görevler, reaktif planlama içermeyen önceden tanımlanmış operasyonlar. | Uçuş esnasında gerçek zamanlı yeniden önceliklendirme ve dinamik ortama uyum. |
| **Haberleşme Arayüzü** | Görüş hattı (LoS), tek yönlü telemetri veya yer kontrol istasyonu (GCS) telsiz bağı. | V2X ağları, sürü düzeyinde koordinasyon, uç-bulut (edge-cloud) senkronizasyonu. |

---

## 4. İnsansız Hava Araçlarında (UAV) VLA ve Öğrenilmiş Kontrol Sistemleri
Hava robotlarında VLA modelleri, milisaniyelik gecikme kısıtları ($\ge 100\text{ Hz}$) ve dış mekanın 3 boyutlu dinamik koşulları altında görev yapmaktadır:

* **Uçtan Uca Görsel-Dilsel Navigasyon (UAV-VLA, CognitiveDrone, RaceVLA):** UAV-VLA uydu/hava görüntülerinden 100 bin uçuşluk görev planı üretebilir. CognitiveDrone, birinci şahıs kamerasından doğrudan 4B eylem ($x, y, z, \text{yaw}$) üretirken; CoT muhakemesi eklenen R1 varyantıyla karmaşık bilişsel görevleri çözer. RaceVLA ise uzman pilot verilerini "agresif apeks dönüşü" gibi sözel komutlarla eşleyerek insan benzeri yarış yörüngeleri oluşturur.
* **Hava Manipülasyonu ve Çift Kol Entegrasyonu (DroneVLA, AIR-VLA, Flying Hand):** Hava araçlarının uçarken manipülatörle nesne yakalamasını sağlar. Flying Hand, tam tahrikli bir hekzarotor üzerine 4-DoF kol yerleştirerek ACT (Action Chunking with Transformers) yönteminin hava araçlarına uyarlanabileceğini kanıtlamıştır.
* **Düşük Gecikmeli Görev Planlama (TypeFly, AeroAgent):** LLM'lerin serbest kod üretimindeki gecikmeyi azaltmak için modeli MiniSpec adı verilen yalın bir drone komut dilinde çıktı vermeye kısıtlayarak planlama gecikmesini 500 ms'nin altına indirmiştir.

<img width="700" alt="UAV Pipeline ve Modeller" src="https://github.com/user-attachments/assets/uav-pipeline-placeholder" />

### Model Gruplarının Karşılaştırması

| Model Grubu | Temsili Modeller | Temel Eylem Mekanizması | Kontrol Frekansı | Odaklandığı Zorluk |
| :--- | :--- | :--- | :--- | :--- |
| **Bimanual (Çift Kol)** | ACT, $\pi_0$, Diffusion Policy | Eylem Parçalama (Chunking), Akış Eşleştirme | Yüksek (30–50 Hz) | 14+ DoF senkronizasyonu, nesne temas dinamiği |
| **UAV (Drone)** | UAV-VLA, AerialVLA | İki Kademeli (Dual-System) Hızlı Başlıklar | Çok Yüksek (>50 Hz) | Milisaniyelik uçuş gecikmesi, rüzgâr/dinamik sapmalar |
| **Genel / Melez** | OpenVLA, RT-2 | Otoregresif / Difüzyon Füzyonu | Düşük-Orta (5–15 Hz) | Geniş kavram dağarcığı, açık dünya sıfır örnekli transfer |

---

## 5. Kaynakça
[1] NVIDIA, "What is Reasoning VLA (Vision-Language-Action)?," NVIDIA Glossary, 2026. [Çevrimiçi]. Erişilebilir: https://www.nvidia.com/en-us/glossary/reasoning-vision-language-action/[cite: 1]

[2] Exxact Corp., "Vision Language Action (VLA) Models Powering Robotics of Tomorrow," Exxact Blog, 23 Ekim 2025. [Çevrimiçi]. Erişilebilir: https://www.exxactcorp.com/blog/deep-learning/vision-language-action-vla-models-powers-robotics[cite: 2]

[3] D. Zhang ve diğ., "Reasoning-VLA: A Fast and General Vision-Language-Action Reasoning Model for Autonomous Driving," arXiv preprint arXiv:2511.19912v1, 25 Kasım 2025.[cite: 3]

[4] Emergent Mind, "Reasoning Vision Language Action (VLA) Models," Emergent Mind Topics, 2026. [Çevrimiçi]. Erişilebilir: https://www.emergentmind.com/topics/reasoning-vision-language-action-vla-models[cite: 4]

[5] I. Sa, C. Park, H.-M. Lee, D. Noh, ve H. S. Ahn, "Vision–Language–Action (VLA) Models for Unmanned Aerial Robotics and Bimanual Manipulation: A Review," Drones, cilt 10, no. 6, s. 412, Mayıs 2026, doi: 10.3390/drones10060412.

[6] I. Sa ve diğ., "Vision–Language–Action (VLA) Models for Unmanned Aerial Robotics and Bimanual Manipulation: A Review," arXiv preprint arXiv:2607.06706, 7 Temmuz 2026.

[7] A. Lykov ve diğ., "CognitiveDrone: A VLA Model and Evaluation Benchmark for Real-Time Cognitive Task Solving and Reasoning in UAVs," arXiv preprint arXiv:2503.01378v1, 3 Mart 2025.

[8] A. Lykov ve diğ., "CognitiveDrone: A VLA Model and Evaluation Benchmark for Real-Time Cognitive Task Solving and Reasoning in UAVs," Hugging Face Papers, 6 Mart 2025. [Çevrimiçi]. Erişilebilir: https://huggingface.co/papers/2503.01378

[9] wazder, "CognitiveDrone Enhanced Reasoning Pipeline," GitHub Repository, 2026. [Çevrimiçi]. Erişilebilir: https://github.com/wazder/cognitive-drone

[10] Robotics Center, "Best VLA Models 2026: Complete Vision-Language-Action Guide," Robotics Center Guides, Nisan 2026. [Çevrimiçi]. Erişilebilir: https://www.roboticscenter.ai/vla-models/best-2026

[11] OpenVLA Team, "OpenVLA-7B Model Card," Hugging Face Hub, 2024. [Çevrimiçi]. Erişilebilir: https://huggingface.co/openvla/openvla-7b

[12] IBM, "What is Chain-of-Thought Prompting?," IBM Think Topics, 2026. [Çevrimiçi]. Erişilebilir: https://www.ibm.com/think/topics/chain-of-thoughts

[13] Z. Yuan ve diğ., "AutoDrive-R: Incentivizing Reasoning and Self-Reflection Capacity for VLA Model in Autonomous Driving," arXiv preprint arXiv:2506.08045v1, Haziran 2025.

[14] DeepLearning.AI, "The Batch: Reasoning Models Transformation," DeepLearning.AI Newsletters, 2025. [Çevrimiçi]. Erişilebilir: https://www.deeplearning.ai/the-batch/reasoning-models-beginning-with-openais-o1-and-deepseeks-r1-transformed-the-industry

[15] A. Lykov ve diğ., "CognitiveDrone Project Page and Benchmark Environment," CognitiveDrone GitHub Pages, Mart 2025. [Çevrimiçi]. Erişilebilir: https://cognitivedrone.github.io/

[16] X. Wang ve diğ., "A Comprehensive Survey and Reference Architecture for AI-Powered Autonomous Drone Systems in Smart Cities," ResearchGate Technical Reports, 2025. [Çevrimiçi]. Erişilebilir: http://www.researchgate.net/
