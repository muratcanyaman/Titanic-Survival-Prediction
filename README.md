# Titanic Survival Prediction

Bu depo, Kaggle Titanic yarışması için hazırlanmış sade bir analiz ve modelleme çalışmasını içerir.

Notebook içinde şu adımlar yer alır:

- eğitim ve test verisini yükleme
- temel ve gelişmiş EDA
- birkaç basit özellik üretimi
- kısa model karşılaştırması
- en iyi modeli kullanarak `submission.csv` oluşturma

Ana notebook dosyası `notebook/Titanic_Kaggle.ipynb` konumundadır.

## Proje Yapısı

```text
Titanic-Survival-Prediction/
data/raw/train.csv
data/raw/test.csv
notebook/Titanic_Kaggle.ipynb
notebook/submission.csv
README.md
```

## Kullanılan Modeller

Notebook içinde şu modeller karşılaştırılır:

- Logistic Regression
- Random Forest
- Gradient Boosting
- Soft Voting

## Çalıştırma

1. Gerekli Python kütüphanelerini kurun: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`
2. `notebook/Titanic_Kaggle.ipynb` dosyasını açın
3. Tüm hücreleri çalıştırın
4. Oluşan `submission.csv` dosyasını Kaggle'a yükleyin

## Notlar

- Notebook kısa ve okunabilir olacak şekilde düzenlenmiştir.
- Ağır hyperparameter tuning yerine daha anlaşılır bir akış tercih edilmiştir.
- EDA kısmı veri yapısını hızlıca görmek için eklenmiştir.
- Score: 0.77033