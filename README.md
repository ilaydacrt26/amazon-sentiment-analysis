# Amazon Yorumları Duygu Analizi

Bu proje, Amazon ürün yorumları üzerinde Doğal Dil İşleme (NLP) teknikleri kullanarak duygu analizi gerçekleştirmeyi amaçlamaktadır. Proje kapsamında, metin verisi ön işleme, kural tabanlı duygu analizi (VADER) ve makine öğrenmesi (Lojistik Regresyon ve Random Forest) yöntemleri uygulanmıştır.

## İş Akışı

Proje aşağıdaki adımları içermektedir:

1.  **Dosya Okuma:** `amazon.xlsx` dosyası bir Pandas DataFrame'e yüklenir.
2.  **Veri Ön İşleme (Data Preprocessing):**
    * Tüm yorumlar küçük harfe çevrilir.
    * Noktalama işaretleri kaldırılır.
    * Sayısal ifadeler metinden çıkarılır.
    * İngilizce `stopwords` (etkisiz kelimeler) kaldırılır.
    * Az geçen (nadir) kelimeler (1 veya daha az görünen) metinden çıkarılır.
    * Kelimeler köklerine indirgenir (Lemmatization).
3.  **Metin Görselleştirme:**
    * En sık kullanılan kelimeleri göstermek için bir bar grafiği oluşturulur.
    * Yorumların bir kelime bulutu (WordCloud) oluşturulur.
4.  **Duygu Analizi (VADER):**
    * NLTK'nın `SentimentIntensityAnalyzer` (VADER) aracı kullanılarak her yorum için bir `polarity_score` (bileşik duygu puanı) hesaplanır.
    * Puanı 0'dan büyük olan yorumlar 'pos' (pozitif), diğerleri 'neg' (negatif) olarak etiketlenir.
5.  **Makine Öğrenmesi ile Modelleme:**
    * Veri, TF-IDF Vectorizer kullanılarak vektörleştirilir.
    * Veri seti eğitim (`X_train`, `y_train`) ve test (`X_test`, `y_test`) olarak ikiye ayrılır.
    * Bir **Lojistik Regresyon** modeli eğitilir.
    * Bir **Random Forest** modeli eğitilir.
6.  **Değerlendirme:**
    * **Lojistik Regresyon:** Test verisi üzerinde **%90** doğruluk (accuracy) ve 5 katlı çapraz doğrulama (Cross-validation) ile ortalama **%88.7** doğruluk elde etmiştir.
    * **Random Forest:** Test verisi üzerinde **%91** doğruluk (accuracy) ve 5 katlı çapraz doğrulama ile ortalama **%91.2** doğruluk elde etmiştir.

## Gereksinimler

Bu projeyi çalıştırmak için aşağıdaki kütüphanelerin kurulu olması gerekmektedir:

* `pandas`
* `openpyxl`
* `nltk`
* `textblob`
* `wordcloud`
* `matplotlib`
* `scikit-learn` (sklearn)

## Kurulum ve Çalıştırma

1.  Gerekli kütüphaneleri yükleyin:
    ```bash
    pip install pandas openpyxl nltk textblob wordcloud matplotlib scikit-learn
    ```

2.  NLTK veri paketlerini indirin (notebook içinde de yapılmaktadır):
    ```python
    import nltk
    nltk.download('stopwords')
    nltk.download('vader_lexicon')
    nltk.download('wordnet')
    ```

3.  `main.ipynb` dosyasını bir Jupyter ortamında açın ve hücreleri sırayla çalıştırın. (Not: `amazon.xlsx` dosyasının notebook ile aynı dizinde olması gerekmektedir.)
