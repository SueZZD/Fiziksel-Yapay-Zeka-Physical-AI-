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
Fiziksel yapay zeka; sensörler ve mekanik sistemler vasıtasıyla fiziksel dünyayla bütünleşik çalışan bir yapay zeka mimarisidir. Ne salt yazılımdan ne de sadece donanımdan ibaret olan bu hibrit yapı; çevresini algılar, elde ettiği verileri işleyerek düşünür ve buna uygun eyleme dönüşen kararlar alır. 
Aklımızda daha iyi yer etmesi için önce günümüzde sıklıkla kullandığımız geleneksel yapay zeka ve robotik sistemlerle ufak bir kıyasını yaparak başlayalım:

### Geleneksel YZ vs. Fiziksel YZ
| Kriter | Geleneksel Yapay Zeka | Fiziksel Yapay Zeka |
| :--- | :--- | :--- |
| **Faaliyet Ortamı** | Sadece dijital ortamlarda bulunur (örn. LLM, veri analitiği)[cite: 2]. | Hem dijital hem de fiziksel alanlarda faaliyet gösterir[cite: 2]. |
| **Veri İşleme** | Statik/asenkron metinler, görüntüler ve dijital loglar[cite: 2]. | Gerçek dünyada dinamik sensör akışı ve fiziksel etkileşim[cite: 2]. |
| **Çıktı Formatı** | Bilgi, metin üretimi veya sanal tahminler[cite: 2]. | Tork değerleri, motor akımları ve mekanik yönlendirme komutları[cite: 2]. |
| **Otonomi** | İnsan yönlendirmesine tabidir[cite: 2]. | Gerçek zamanlı otonom karar alır[cite: 2]. |

---

## 2. Temel Mimari: Algılama, Zeka ve Eylem Döngüsü
Önceden programlanmış katı komutlarla hareket eden geleneksel robotik sistemlerin aksine bu teknoloji; çevresel değişikliklere esnek bir biçimde yanıt verebilen ve deneyimledikçe kendi kendine öğrenebilen entegre bir sistem sunar. Çalışma prensibi insan biyolojisinden ilham alan sürekli bir döngüye dayanır: Sistem; kameralar, LiDAR ve dokunma sensörleriyle çevreyi algılar, büyük görsel-dil modelleri ve pekiştirmeli öğrenme (reinforcement learning) aracılığıyla elde ettiği veriyi yorumlayıp karar alır ve son olarak bu kararları mekanik donanımları üzerinden gerçek dünyada somut fiziksel eylemlere dönüştürür [3].
Fiziksel yapay zeka sistemi tipik olarak üç ana yeteneğe sahiptir:
•	Kameralar, mikrofonlar, LiDAR veya diğer sensörler aracılığıyla çevreyi algılama
•	Olan biteni yorumlayan fiziksel yapay zeka modelleri kullanarak bilgileri işleme.
•	Robotlar, makineler veya otomatik sistemler aracılığıyla alınan kararlara göre hareket etmek [3].

<img width="791" height="662" alt="image" src="https://github.com/user-attachments/assets/56ce698f-475c-4456-b111-3b1a9ebc0967" />

Endüstriyel ve toplumsal ölçekte dönüştürücü bir etkiye sahip olan Fiziksel Yapay Zeka; akıllı şehir altyapılarında, otonom araçlarda, lojistik operasyonlarında, akıllı fabrikalarda ve sağlık sektöründe (hassas cerrahi robotları ve hasta bakım asistanları) giderek daha fazla uygulama alanı bulmaktadır. Bununla birlikte, teknolojinin tam potansiyeline ulaşarak yaygınlaşabilmesi için simülasyon ortamları ile gerçek dünya arasındaki veri uyuşmazlıklarının (domain gap) aşılması, sensör hassasiyeti ve batarya verimliliği gibi donanımsal sorunların çözülmesi gerekmektedir. Ayrıca, operasyonel güvenliğin temin edilmesi, veri gizliliğinin korunması ve iş gücü piyasasındaki sosyo-ekonomik dönüşümün yönetilebilmesi adına, kapsamlı yasal düzenlemelerin ve insan-makine iş birliği standartlarının oluşturulması kritik bir zorunluluk olarak öne çıkmaktadır [1, 3]. 
Fiziksel yapay zekaya daha derinlemesine bir giriş yapalım ve kullanıldığı alanları, hangi modeller aracılığı ile geliştirilip nasıl bir sistem dahilinde hizmete sunulduğunu, yani teknik yönünü, ve gerçekleştirilmesi karşısındaki zorlukları inceleyelim.

---

## 3. İnsansı Robotlar ve Gelişmiş Donanım Entegrasyonu (Helix 02)
İnsansı robotlar, insan vücut yapısına merkeze alarak modellenmiş ve insanlarla beraber çalışarak verimliliği artırmak üzere tasarlanmış, genel amaçlı, iki ayaklı robotlardır. Nesne kavrayabilir, konteyner taşıyabilir, kutuları yükleyip boşaltabilir ve bunların dışında çeşitli görevleri öğrenme ve gerçekleştirme yeteneğine sahiptirler [5].
Son zamanlarda geliştirilmiş bazı insansız robotları inceleyelim.
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

**1. Uç Bilişim (Edge AI) ve Yerleşik Sistem Kısıtlamaları**
•	Bulut altyapısına olan bağımlılığı ortadan kaldıran Uç Yapay Zeka (Edge AI), otonom makinelerde anlık karar alma süreçleri için kritik olan düşük gecikmeli (low-latency) çıkarım ve gerçek zamanlı veri işleme imkanı sunar.
•	Otomotiv standartlarındaki donanımların sınırları göz önüne alındığında, Microsoft'un Phi-4-mini-instruct gibi yerel modelleri; bellek ve işlem gücünün kısıtlı olduğu, gecikmeye son derece duyarlı (latency-bound) senaryolarda yüksek matematiksel ve mantıksal akıl yürütme kapasitesi sağlamak üzere tasarlanmıştır.
•	Araç içi deneyimde ise Mercedes-Benz'in MBUX sistemi, bulut bağlantısı ve gelişmiş ses kontrolünü birleştirerek, koltuk pozisyonlarından aracın sürüş modlarına kadar geniş bir araç dinamiği ağını duyarlı bilgisayar işlemcileriyle kontrol etmektedir.


**2. Çok Modlu Mimari: LLM, VLM ve VLA Arasındaki Geçiş**
•	Sadece metin işleme üzerine kurulu olan Büyük Dil Modellerinin (LLM) aksine, Görsel-Dil Modelleri (VLM) kamera verisi ile metni entegre ederek çok modlu yapıları anlamlandırır.
•	Görsel-Dil-Eylem (VLA) modelleri ise bu yapıyı bir adım öteye taşıyarak, algılanan çevresel verileri ve metin komutlarını otonom araçlar veya robotik sistemler için doğrudan fiziksel eylemlere dönüştürür.
•	Bu doğrultuda gelişen Robotik Temel Modelleri (RFM) hiyerarşik bir yapı kullanır: Sensör verisini işleyen algılama (perception) katmanı, mantıksal görevleri düzenleyen planlama (planning) katmanı ve istenen durum hedeflerine ulaşmak için düşük seviyeli motor komutlarını uygulayan kontrol (control) katmanı.


**3. Otonom Araç Planlamasında Fiziksel Yapay Zeka Kullanımı**
•	Fiziksel Yapay Zeka, temel dil ve görüş modellerinin robotik donanımlarla buluştuğu noktadır; açık kaynaklı VLA modelleri (örneğin OpenVLA) ile doğrudan eylem politikaları (ACT policy) geliştirilerek karmaşık görevler yerel donanımlarda eğitilebilmektedir.
•	Otonom araç geliştirme süreçleri için tasarlanan NVIDIA Alpamayo 2 Super gibi VLA modelleri, çoklu kameralardan gelen 360 derecelik algı verilerini işleyerek aracın gelecekteki hedef yörüngelerini (trajectory) doğrudan üretebilir.
•	VLA sistemleri sadece kontrol referansı üretmekle kalmaz; aynı zamanda "Neden-Sonuç Zinciri" (Chain-of-Causation) mekanizması ile şerit değiştirme, yavaşlama veya durma gibi yüksek seviyeli eylemlerin arkasındaki akıl yürütme süreçlerini geriye dönük olarak açıklayabilir.
•	Yine de bu modellerin donanım seviyesinde entegrasyonunda; çok adımlı karmaşık görevlerdeki uzamsal ve zamansal akıl yürütme (spatial and temporal reasoning) kapasitesinin, mevcut çip kısıtlamaları altında stabil tutulması en büyük zorluklardan biri olarak öne çıkmaktadır.


---

## 6. Uç Bilişim (Edge AI) ve Phi-4-mini-instruct Entegrasyonu
Saniyenin onda biri gibi kritik gecikme sürelerini tolere edemeyen otonom sistemlerde bulut bağımlılığı ortadan kaldırılmalıdır[cite: 2]. 
Araştırma kapsamında incelenen Microsoft **Phi-4-mini-instruct** modeli; 3.8 Milyar parametreli bir SLM (Small Language Model) olmasına karşın sunduğu **128k token bağlam uzunluğu (context window)** sayesinde[cite: 2]; CAN-BUS log ağlarının incelenmesi, ROS 2 düğümlerinin analizi ve gömülü sistem optimizasyonlarında donanım sınırlarını zorlamadan bütüncül analiz imkanı tanır[cite: 2].

---

## 7. Kaynakça
*[1] NVIDIA, "Generative Physical AI," NVIDIA Glossary, 2026. URL: https://www.nvidia.com/en-us/glossary/generative-physical-ai/

[2] Archetype AI, "What Is Physical AI," Archetype AI Guides, 2026. URL: https://www.archetypeai.io/guides/what-is-physical-ai

[3] Liahnson, "What Is Physical AI: Understanding the Concept, Principles, Applications, and Future Outlook," Liahnson Insights, 2026. URL: https://liahnson.com/insights/what-is-physical-ai-understanding-the-concept-principles-applications-and-future-outlook/

[4] Acrosser, "How Physical AI Differs From Robotics," Acrosser Technology, 2026. URL: https://www.acrosser.com/how-physical-ai-differs-from-robotics.html

[5] NVIDIA, "Humanoid Robot," NVIDIA Glossary, 2026. URL: https://www.nvidia.com/en-us/glossary/humanoid-robot/

[6] Boston Dynamics, "Atlas," Boston Dynamics Products, 2026. URL: https://bostondynamics.com/products/atlas/

[7] Austin Business Journal, "Diligent Robotics Launches New Hospital Robot HQ," BizJournals, Aug. 2026. URL: https://www.bizjournals.com/austin/news/2026/08/17/diligent-robotics-launches-new-hospital-robot-hq.html

[8] Diligent Robotics, "Moxi2: Physical AI Healthcare Robotics," LinkedIn Activity, 2026. URL: https://www.linkedin.com/posts/diligent-robotics_moxi2-physicalai-healthcarerobotics-activity-7495095236679905280-fVGD

[9] Cerence, "Cerence Generative AI In-Car Experience," NVIDIA DGX Cloud Resources, 2026. URL: https://resources.nvidia.com/en-us-dgx-cloud/cerence-generative-ai-in-car-experience

[10] FEV, "FEV Collaborates With Microsoft on Efficient AI Model Approach for In-Car Applications Built on NVIDIA," FEV Press Release, 2026. URL: https://www.fev.com/en/fev-collaborates-with-microsoft-on-efficient-ai-model-approach-for-in-car-applications-built-on-nvidia/

[11] Wayve, "Wayve: Embodied AI for Autonomous Driving," Wayve.ai, 2026. URL: https://wayve.ai/

[12] F. Pope, "Tesla FSD 12," Machine Learning Blog, 2026. URL: https://www.fredpope.com/blog/machine-learning/tesla-fsd-12

[13] ResearchGate, "Robotic Foundation Models and Physical AI: Innovations, Applications, Ethical Challenges, and the Future of Generalized Robotics," ResearchGate, Publication 388178070, 2026. URL: https://www.researchgate.net/publication/388178070_Robotic_Foundation_Models_and_Physical_AI_Innovations_Applications_Ethical_Challenges_and_the_Future_of_Generalized_Robotics

[14] Robotics Center, "Physical AI 2026 Guide," Robotics Center Blog, 2026. URL: https://www.roboticscenter.ai/blog/physical-ai-2026-guide

[15] A. Pipal, "LLM, VLM, and VLA," Medium, 2026. URL: https://medium.com/@arpipal2/llm-vlm-and-vla-d758b91479eb

[16] NVIDIA, "Reasoning Vision Language Action (rVLA)," NVIDIA Glossary, 2026. URL: https://www.nvidia.com/en-us/glossary/reasoning-vision-language-action/

[17] IBM, "Edge AI," IBM Think Topics, 2026. URL: https://www.ibm.com/think/topics/edge-ai

[18] Exxact Corp, "Vision-Language-Action (VLA) Models Powers Robotics," Exxact Corp Blog, 2026. URL: https://www.exxactcorp.com/blog/deep-learning/vision-language-action-vla-models-powers-robotics

[19] Windows Forum, "FEV and Microsoft Bring Phi-4-Mini-Instruct Local AI to NVIDIA Drive AGX," Windows News, 2026. URL: https://windowsforum.com/windows-news.4/fev-and-microsoft-bring-phi-4-mini-instruct-local-ai-to-nvidia-drive-agx.436315/

[20] Arabam.com, "MBUX Bilgi Eğlence Sistemi: Mercedes Kullanıcı Deneyimi," Arabam Blog, 2026. URL: https://www.arabam.com/blog/genel/mbux-bilgi-eglence-sistemi-mercedes-kullanici-deneyimi/

[21] Microsoft, "Phi-4-Mini-Instruct," Hugging Face, 2026. URL: https://huggingface.co/microsoft/Phi-4-mini-instruct

[22] NVIDIA, "Deep Learning for Self-Driving Cars," NVIDIA Developer Blog, 2026. URL: https://developer.nvidia.com/blog/deep-learning-self-driving-cars/

[23] Windows Forum, "FEV and Microsoft Bring Phi-4-Mini-Instruct Local AI to NVIDIA Drive AGX," Windows News, 2026. URL: https://windowsforum.com/windows-news.4/fev-and-microsoft-bring-phi-4-mini-instruct-local-ai-to-nvidia-drive-agx.436315/

[24] arXiv, "Preprint 2101.02082," arXiv preprint, arXiv:2101.02082, 2021. URL: https://arxiv.org/abs/2101.02082

[25] Digital Divide Data, "In-Cabin AI: Why Driver Condition & Behavior Annotation Matters," DDD Blog, 2026. URL:https://www.digitaldividedata.com/blog/in-cabin-ai-why-driver-condition-behavior-annotation-matters

[26] InCabin, "AI Systems: Real-Time Safety at the Edge," InCabin Blog, 2026. URL: https://incabin.com/blog/ai-systems-real-time-safety-at-the-edge/

[27] BMW Group, "Press Release: T0455864EN," BMW Group PressClub, 2026. URL: https://www.press.bmwgroup.com/global/article/detail/T0455864EN/

[28] BMW Group, "Press Release: T0458778EN," BMW Group PressClub, 2026. URL: https://www.press.bmwgroup.com/global/article/detail/T0458778EN/

[29] Microsoft Azure, "Empowering Innovation: The Next Generation of the Phi Family," Azure Blog, 2026. URL: https://azure.microsoft.com/en-us/blog/empowering-innovation-the-next-generation-of-the-phi-family/

[30] Strategy& (PwC), "Physical AI," PwC Industries TMT, 2026. URL: https://www.strategyand.pwc.com/de/en/industries/telecommunication-media-and-technology/physical-ai.html
*
