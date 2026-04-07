# 🚢 Titanic Hayatta Kalma Tahmini (Titanic Survival Prediction)

Bu depo (repository), Kaggle'ın makine öğrenmesine giriş niteliğindeki efsanevi yarışması olan [Titanic - Machine Learning from Disaster](https://www.kaggle.com/c/titanic) için hazırladığım **uçtan uca veri bilimi pipeline'ını** ve kurguladığım makine öğrenmesi modellerini içerir.

---

## 📋 Proje Özeti
Projenin temel amacı, gemideki yolcuların demografik (yaş, cinsiyet) ve seyahat (bilet sınıfı, aile büyüklüğü) verilerini analiz ederek **kimlerin kazadan sağ kurtulduğunu (Survival: 0 veya 1) tahmin etmektir.** 

Çalışma kapsamında sırasıyla şu *Veri Bilimi ve Makine Öğrenmesi (Machine Learning)* adımları uygulanmıştır:
1. **Veri Keşfi ve Görselleştirme (EDA):** Verilerdeki istatistiksel dağılımlar incelendi ve sağ kalım üzerindeki etkiler (Cinsiyet, Pclass vb.) tespit edildi.
2. **Özellik Mühendisliği (Feature Engineering):** Yolcu Unvanları (Title), Aile Boyutu (FamilySize) ve Yalnızlık Durumu (IsAlone) gibi veriye değer katan yepyeni sinyaller/özellikler türetildi. 
3. **Eksik Veri Yönetimi (Imputation):** Yaş ve Bilet Ücreti sütunlarındaki eksik (NaN) veriler, basit bir medyan yerine "Unvan" ve "Bilet Sınıfına" göre gruplanıp, çok daha akıllıca (Grup Medyanı) dolduruldu.
4. **Gelişmiş Modelleme (Ensemble Learning):** Farklı algoritmaların güçlü yönlerini birleştiren gelişmiş bir Topluluk (Ensemble) Modeli kuruldu.

---

## ⚙️ Model Algoritmaları ve Yaklaşım
Verideki kalıpları ezberlemeden (overfitting olmadan) öğrenebilmek için **Yumuşak Oylama Sınıflandırıcısı (Soft Voting Classifier)** yöntemi kullanılmış, birbirinin eksiklerini başarılı şekilde kapatan şu üç devasa temel ağaç ve diferansiyel model bir araya getirilmiştir:

*   🌲 **Random Forest Classifier:** Bagging mantığıyla çalışarak varyansı düşük, iyi genellenmiş ağaç bazlı sağlam kararlar verir.
*   🚀 **XGBoost Classifier:** Gradient Boosting mantığıyla ağırlıklandırarak önceki ağaçların hatalarından öğrenir ve tahmini keskinleştirir.
*   📉 **Support Vector Machine (SVC):** Ağaç algoritmalarının göremediği doğrusallıktan uzak (non-linear) karmaşık sınırları çizer *(Pipeline içinde öncelikle StandardScaler ile boyutlandırılarak kullanılmıştır)*.

---

## 📁 Proje Klasör Yapısı
\`\`\`text
Titanic-Survival-Prediction/
├── data/
│   └── raw/
│       ├── train.csv             # Eğitim verisi ve hedefler (Survived sütunu)
│       └── test.csv              # Model tarafından tahmin edilmesi gereken test verisi
├── notebooks/
│   └── Titanic_Kaggle.ipynb      # Yapılan bütün analizleri ve Topluluk (Ensemble) modelini içeren "Ana Jupyter Notebook"
└── README.md                     # Projenin Markdown sunum dosyası
\`\`\`

---

## 🚀 Projeyi Çalıştırma (Kullanım Rehberi)
Projeyi kendi bilgisayarınızda derleyip incelemek isterseniz aşağıdaki adımları izleyebilirsiniz:

1. Bu projeyi bilgisayarınıza klonlayın:
   \`\`\`bash
   git clone https://github.com/KULLANICI_ADINIZ/Titanic-Survival-Prediction.git
   \`\`\`
2. Python ortamınızda temel Veri Bilimi kütüphanelerinin (`pandas`, `numpy`, `scikit-learn`, `xgboost`, `seaborn`, `matplotlib`) kurulu olduğundan emin olun.
3. Jupyter Notebook veya VSCode ortamınız üzerinden `notebooks/Titanic_Kaggle.ipynb` dosyasını açın.
4. En üst menüden **Run All (Tümünü Çalıştır)** diyerek kodun veriyi nasıl işlediğini, görselleştirdiğini ve en sonunda da **`submission.csv`** tahmin dosyasını nasıl oluşturduğunu izleyebilirsiniz.

---

## 📊 Özet Sonuçlar ve Analitik Çıkarımlar
Kaggle teslim (Submission) sistemine yüklenen model, **%77.0+ (0.77 Accuracy)** doğruluk oranına ulaşarak, ezberden tamamen uzak son derece sağlıklı ve sağlam bir **Baseline (Temel Skor)** elde etmeyi başarmıştır. Modelin üretimi sırasında herhangi bir veri sızıntısı (Data Leakage) yapılmamıştır.

Modelin ürettiği çıkarımlar ve EDA (Keşifsel Veri Analizi) ışığında Titanic felaketine dair temel tespitler şunlardır:
* **"Önce Kadınlar ve Çocuklar":** En yüksek hayatta kalma oranına "Kadınlar" ve "Master" unvanını taşıyan çocuk yolcular sahiptir.
* **Sosyo-Ekonomik Sınıf Etkisi (Pclass):** 1. sınıf (First Class) lüks yolcuların hayatta kalma ihtimali, 3. sınıf (Third Class) sahiplerine kıyasla bariz şekilde çok daha yüksektir.
* **Aile Büyüklüğü (FamilySize):** Gemiye tek başına binenler veya çok kalabalık (6+ kişi) binenlerin hayatta kalma oranları, "çekirdek aile (2-4 kişi)" olarak seyahat edenlere göre trajik şekilde daha düşüktür. Ailenin büyük olması lojistik hareket kabiliyetini sıfırlarken, tek olmak yardımlaşma ve haber alma ihtimalini düşürüp dezavantaj getirmiştir.
