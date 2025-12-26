# Sephora Kozmetik Ürünleri Veri Madenciliği

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=for-the-badge&logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-green?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data-purple?style=for-the-badge&logo=pandas&logoColor=white)

**1,472 Sephora ürünü üzerinde kapsamlı veri analizi ve makine öğrenmesi**

[Keşifsel Analiz](#-keşifsel-veri-analizi) •
[Kümeleme](#-kümeleme-analizi) •
[Sınıflandırma](#-sınıflandırma) •
[Sonuçlar](#-temel-bulgular)

</div>

---

## Proje Hakkında

Bu projede **Kaggle Sephora Cosmetics** veri seti üzerinde kapsamlı bir veri madenciliği çalışması gerçekleştirilmiştir. Proje, kozmetik ürünlerinin fiyat, puan, içerik ve cilt tipi uygunluğu gibi özelliklerini analiz ederek anlamlı örüntüler keşfetmeyi amaçlamaktadır.

### Veri Seti Özellikleri

| Özellik | Değer |
|---------|-------|
| Toplam Ürün | 1,472 |
| Marka Sayısı | 116 |
| Kategori Sayısı | 6 |
| Fiyat Aralığı | $3 - $370 |
| Ortalama Puan | 4.15 / 5.0 |

---

## Metodoloji

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Veri Toplama  │ ──▶ │   Ön İşleme     │ ──▶ │  Veri Madenciliği│ ──▶ │   Yorumlama    │
│                 │     │                 │     │                 │     │                 │
│  • Kaggle API   │     │  • Temizleme    │     │  • K-Means      │     │  • İş Önerileri │
│  • CSV Import   │     │  • Encoding     │     │  • Decision Tree│     │  • Raporlama    │
│                 │     │  • Scaling      │     │  • Random Forest│     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

---

## Keşifsel Veri Analizi

### Ürün Kategorileri

| Kategori | Ürün Sayısı | Oran |
|----------|-------------|------|
| Moisturizer | 298 | %20.2 |
| Cleanser | 281 | %19.1 |
| Face Mask | 266 | %18.1 |
| Treatment | 248 | %16.8 |
| Eye Cream | 209 | %14.2 |
| Sun Protect | 170 | %11.6 |

### Cilt Tipi Uygunluğu

```
Normal      ████████████████████████████████  959 ürün (%65)
Combination ████████████████████████████████  966 ürün (%66)
Dry         ███████████████████████████████   899 ürün (%61)
Oily        ███████████████████████████████   893 ürün (%61)
Sensitive   ██████████████████████████        751 ürün (%51)
```

### En Popüler Markalar

1. **CLINIQUE** - 79 ürün
2. **SEPHORA COLLECTION** - 66 ürün
3. **SHISEIDO** - 63 ürün
4. **ORIGINS** - 54 ürün
5. **MURAD** - 47 ürün

---

## Kümeleme Analizi

**K-Means** algoritması ile ürünler 4 farklı kümeye ayrılmıştır:

| Küme | Ürün Sayısı | Ort. Fiyat | Profil |
|------|-------------|------------|--------|
| 0 | 74 | $188.61 | Premium/Lüks segment, tüm cilt tiplerine uygun |
| 1 | 511 | $51.53 | Ekonomik, belirli cilt tiplerine özel |
| 2 | 866 | $46.45 | Orta segment, geniş cilt tipi uyumluluğu |
| 3 | 21 | $62.14 | Niş ürünler, düşük puanlı |

**Silhouette Score: 0.5964** (İyi kümeleme kalitesi)

---

## Sınıflandırma

Fiyat kategorisi tahmini için iki model eğitilmiştir:

### Model Performansları

| Model | Accuracy | En İyi Özellik |
|-------|----------|----------------|
| Decision Tree | %46.83 | Ingredient_Count |
| Random Forest | %47.74 | Ingredient_Count |

> **Not:** 4 sınıflı bir problemde rastgele tahmin %25 olduğundan, modeller anlamlı sonuçlar üretmektedir.

### Özellik Önem Sıralaması

```
Ingredient_Count  ████████████████████████  0.42
Label_Encoded     ██████████████████        0.31
Rank              ██████████                0.12
Sensitive         ████                      0.05
Combination       ███                       0.04
...
```

---

## Temel Bulgular

### Fiyat-Kalite İlişkisi
> Fiyat ile puan arasında güçlü bir korelasyon **bulunmamaktadır**.
> Yüksek fiyatlı ürünler her zaman daha yüksek puan almıyor.

### Cilt Tipi Trendleri
> Tüm cilt tiplerine uygun ürünler daha **yaygın** ve **popüler**.

### İçerik Analizi
> Ürün içerik sayısı, fiyat kategorisini belirlemede en önemli faktör.

---

## Kurulum ve Çalıştırma

```bash
# Repository'yi klonla
git clone https://github.com/ahsenyenisey/sephora-cosmetics-data-mining.git

# Dizine gir
cd sephora-cosmetics-data-mining

# Gerekli kütüphaneleri yükle
pip install pandas numpy matplotlib seaborn scikit-learn jupyter

# Jupyter Notebook'u başlat
jupyter notebook cosmetics_analysis.ipynb
```

---

## Proje Yapısı

```
sephora-cosmetics-data-mining/
│
├── cosmetics_analysis.ipynb   # Ana analiz notebook'u
├── cosmetics.csv              # Ham veri seti
├── cosmetics_processed.csv    # İşlenmiş veri seti
├── .gitignore
└── README.md
```

---

## Kullanılan Teknolojiler

- **Python 3.8+**
- **Pandas** - Veri manipülasyonu
- **NumPy** - Sayısal hesaplamalar
- **Matplotlib & Seaborn** - Görselleştirme
- **Scikit-learn** - Makine öğrenmesi
  - K-Means Clustering
  - Decision Tree Classifier
  - Random Forest Classifier
  - PCA (Boyut indirgeme)

---

## Lisans

Bu proje eğitim amaçlı hazırlanmıştır.

---

<div align="center">

**Veri Seti Kaynağı:** [Kaggle - Cosmetics Datasets](https://www.kaggle.com/datasets/kingabzpro/cosmetics-datasets)

</div>
