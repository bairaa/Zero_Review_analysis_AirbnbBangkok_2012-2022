# Analisis Faktor Risiko Zero Review pada Listing Airbnb Bangkok 2012–2022

## Overview

Lebih dari 36% listing Airbnb di Bangkok tidak memiliki satu pun ulasan tamu (*zero review*) — kondisi yang secara langsung menekan visibilitas listing di algoritma pencarian platform dan berdampak pada GMV. Proyek ini menganalisis faktor-faktor apa saja yang berasosiasi dengan tingginya zero review rate, seberapa kuat pengaruhnya, dan segmen mana yang paling rentan sebagai dasar prioritas intervensi.

**Stakeholder:** Host Operations & Performance Team

---

## Pertanyaan Bisnis

1. Apakah terdapat perbedaan yang signifikan secara statistik dalam risiko *zero review* antar kelompok listing berdasarkan wilayah, tipe properti, dan segmen harga?
2. Faktor apa saja yang berasosiasi dengan tingginya *zero review rate*, dan seberapa kuat pengaruhnya?
3. Strategi intervensi apa yang dapat diterapkan untuk mengurangi jumlah listing *zero review*, terutama pada segmen yang paling rentan?

---

## Dataset

| | |
|---|---|
| **Sumber** | [Airbnb Listings Bangkok — Inside Airbnb](http://insideairbnb.com) |
| **Periode** | 2012–2022 |
| **Ukuran** | 15.853 listing (setelah data cleaning) |
| **Variabel dependen** | `is_zero_review` — biner (1 = tidak ada review, 0 = ada review) |

---

## Alur Analisis

```
1. Business Understanding
2. Data Understanding
3. Data Cleaning          → missing values, duplicate coordinates, anomali harga
4. Exploratory Data Analysis
   ├── Univariate Numerik
   └── Univariate Kategorikal + Feature Engineering
          (price_category, location_category, is_zero_review)
5. Inferential Analysis
   ├── 5.1  Seleksi Variabel — Cramér's V + Spearman ρ
   ├── 5.2  Room Type        — Chi-Square + Z-Test Proporsi
   ├── 5.3  Availability     — Kruskal-Wallis + Mann-Whitney U
   ├── 5.4  Host Listings    — Kruskal-Wallis + Mann-Whitney U
   ├── 5.5  Location         — Chi-Square + Z-Test Proporsi
   ├── 5.6  Price            — Chi-Square + Z-Test Proporsi + Spearman
   └── 5.7  Interaksi Room Type × Location — Crosstab + Heatmap
6. Conclusion
7. Business Recommendation
```

---

## Temuan Utama

| Prioritas | Faktor | Kekuatan | Zero Review Rate Tertinggi |
|-----------|--------|----------|---------------------------|
| 1 | Tipe Properti | Cramér's V ≈ 0.26 (Sedang) | Shared room: ~60.8% |
| 2 | Ketersediaan Kalender | Spearman \|ρ\| = 0.24 | Very High (Q4): tertinggi |
| 3 | Skala Portofolio Host | Spearman \|ρ\| = 0.22 | Host Solo: tertinggi |
| 4 | Kategori Lokasi | Cramér's V ≈ 0.11 | Peripheral: ~61.2% |
| 5 | Segmen Harga | Cramér's V ≈ 0.08 | Luxury: ~42.6% |

Kombinasi paling berisiko: **Shared room + Peripheral** (zero review rate tertinggi di seluruh segmen).

---

## Keterbatasan

- Data historis 2012–2022; tidak mencerminkan kondisi pasar pasca-pandemi
- `availability_365` tidak membedakan hari terisi karena *booking* vs *host block*
- Analisis bersifat **deskriptif-asosiatif**, bukan kausal — temuan tidak dapat diinterpretasikan sebagai hubungan sebab-akibat langsung
- Tidak ada data kualitas properti (foto, rating bintang) atau performa host (response rate)
