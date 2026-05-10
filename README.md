# Pnömoni Tespiti — CNN ile Görüntü Sınıflandırma

İstatistiksel Analiz Dersi — Görüntü Verisi Sunum Projesi

## Proje Hakkında

Bu projede chest X-ray görüntüleri üzerinden pnömoni (zatürre) tespiti için **sıfırdan bir CNN modeli** geliştirildi. Transfer learning kullanılmadı; tüm mimari, eğitim ve değerlendirme süreci kendi tasarımımız.

**Dataset:** [Chest X-Ray Pneumonia (Kaggle)](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia)

**Kullanılan Araçlar:** MATLAB R2025b, Deep Learning Toolbox

**Sonuçlar:**
- Validation Accuracy: %95.14
- Test Accuracy: %81.41
- PNEUMONIA Recall: %98.21
- NORMAL Recall: %53.42

## Yazarlar

- [Ferit Can Obuz](https://github.com/feritcanobuz)
- [Cerennr](https://github.com/cerennr)

---

## Cerennr İçin Kurulum Rehberi

Bu rehber, projeye sıfırdan başlayan biri için hazırlanmıştır. Sırayla takip et, atlama yapma.

### 1. Git Bash'i Aç

Windows'ta projeyi koymak istediğin klasöre git (örn. `C:\Users\KULLANICI_ADIN\Documents\`). Klasöre **boş bir alana sağ tık** yap, **"Git Bash Here"** seç. Siyah bir terminal penceresi açılır.

### 2. Repo'yu Klonla

Git Bash'te şu komutu yaz ve Enter:

```bash
git clone https://github.com/feritcanobuz/image-data-presentation.git
```

Klonlama bitince, repo klasörünün içine gir:

```bash
cd image-data-presentation
```

### 3. Klonlanan Klasörü Aç

Dosya gezgininde klonladığın klasörü aç. İçinde şu dosyaları göreceksin:

```
image-data-presentation/
├── .gitignore
├── README.md
├── pneumonia_classification.mlx
└── .git/  (gizli klasör)
```

### 4. Dataset'i İndir ve Yerleştir

Datasetı buradan indir: https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia

İndirdiğin zip'i çıkart. İçinden `chest_xray` klasörünü bul.

**Eğer çıktıda `chest_xray/chest_xray/...` gibi iç içe klasör yapısı varsa**, sadece içteki `chest_xray` klasörünü al.

**Eğer `__MACOSX` adında klasör varsa, onu sil.**

Final yapı şöyle olmalı:

```
chest_xray/
├── test/
│   ├── NORMAL/
│   └── PNEUMONIA/
├── train/
│   ├── NORMAL/
│   └── PNEUMONIA/
└── val/
    ├── NORMAL/
    └── PNEUMONIA/
```

Şimdi:

1. Repo klasöründe (`image-data-presentation/`) **`data` adında yeni bir klasör oluştur**
2. `chest_xray` klasörünü `data` klasörünün içine taşı

Sonuç:

```
image-data-presentation/
├── .gitignore
├── README.md
├── pneumonia_classification.mlx
└── data/
    └── chest_xray/
        ├── test/
        ├── train/
        └── val/
```

### 5. Eğitilmiş Model ve Tahmin Dosyalarını İndir

Ferit'in attığı Drive linkinden iki dosyayı indir:

- `trained_model.mat`
- `test_predictions.mat`

İndirdiğin bu iki dosyayı **doğrudan repo klasörünün ana dizinine** yapıştır:

```
image-data-presentation/
├── .gitignore
├── README.md
├── pneumonia_classification.mlx
├── trained_model.mat       ← buraya
├── test_predictions.mat    ← buraya
└── data/
    └── chest_xray/
```

**Önemli:** Bu iki dosya `.gitignore`'da tanımlı olduğu için GitHub'a yüklenmez, sende yerel olarak duracak.

### 6. MATLAB'i Aç ve Çalışma Klasörünü Ayarla

MATLAB R2025b'yi aç. Üstteki adres çubuğuna repo klasörünün tam yolunu yapıştır:

```
C:\Users\KULLANICI_ADIN\...\image-data-presentation
```

Enter'a bas. Sol tarafta Files panelinde repo dosyalarını görmelisin.

### 7. Live Script'i Aç

Files panelinde `pneumonia_classification.mlx` dosyasına çift tıkla. Live Editor açılır.

### 8. Eğitilmiş Modeli Yükle (CNN'i Tekrar Eğitmeye Gerek Yok!)

**ÇOK ÖNEMLİ:** Modeli sıfırdan eğitmek 23 dakika sürer. Buna gerek yok, çünkü Ferit eğitti ve `trained_model.mat` olarak paylaştı.

Live Script'in en altına in, en son hücreden sonra **yeni bir section break** ekle (LIVE EDITOR sekmesinde "Section Break" butonu). Yeni bir kod hücresi aç ve şu kodu çalıştır:

```matlab
% Eğitilmiş modeli ve tahmin sonuçlarını yükle
load('trained_model.mat');
load('test_predictions.mat');

fprintf('Model ve tahmin sonuçları başarıyla yüklendi.\n');
fprintf('trainedNet: eğitilmiş CNN modeli\n');
fprintf('YPred: test tahminleri\n');
fprintf('YTrue: gerçek etiketler\n');
fprintf('scores: sınıf olasılıkları\n');
```

Bu hücre çalışınca Workspace'te `trainedNet`, `YPred`, `YTrue`, `scores` değişkenlerini göreceksin. Artık bunları kullanarak değerlendirme aşamasına geçebilirsin.

**Önceki hücreleri tek tek çalıştırmana GEREK YOK.** Sadece bu yükleme hücresi yeterli.

---

## Cerennr'ın Yapacakları

Aşağıdaki adımları sırayla tamamla. Her adım yeni bir bölüm olacak Live Script'te.

### Adım 1: Confusion Matrix
### Adım 2: Performans Metrikleri (Accuracy, Precision, Recall, F1, Specificity)
### Adım 3: ROC Eğrisi ve AUC
### Adım 4: Örnek Tahminlerin Görselleştirilmesi (Doğru ve Yanlış Sınıflandırmalar)
### Adım 5: Grad-CAM ile Modelin Bakışının Görselleştirilmesi
### Adım 6: Sonuçların Tartışılması ve Sınırlılıklar

---

## Markdown Eklerken Dikkat Edilecekler

Live Script'te her kod hücresinden önce ve sonra markdown metinleri olmalı.

- **Her bölümün başında** Heading 1 veya Heading 2 başlık ekle (üst dropdown'dan seç)
- **Her kod hücresinden önce** 1-2 cümle açıklama yaz (ne yapacağını anlatan)
- **Her kod hücresinden sonra** 2-3 cümle yorum yaz (çıktıyı yorumlayan)
- Bullet point yerine düz paragraf yazılmalı (sunum formatı için daha temiz)
- Türkçe karakter kullanmaktan çekinme

Mevcut hücrelere bakarsan formatı görürsün, aynı formatı koru.

---

## Claude Sohbetinde Kullanılacak Prompt

Aşağıdaki prompt'u kopyala, yeni bir Claude sohbetine yapıştır. Claude kaldığın yerden devam edip sana adım adım yardımcı olacak.

```
Selam, ekip arkadaşımla beraber bir İstatistiksel Analiz dersi sunumu için MATLAB'de chest X-ray pneumonia detection projesi yapıyoruz. Sıfırdan kendi CNN modelimizi tasarladık ve eğittik.

Şu ana kadar yapılanlar:
1. Veri keşfi (klasör yapısı, sınıf dağılımı, örnek görüntüler)
2. Veri hazırlığı (imageDatastore, train/val yeniden bölme, augmentation)
3. CNN mimarisi tasarımı (4 conv block + FC katmanlar, 6.6M parametre, 23 katman)
4. Eğitim (Adam, lr=1e-4, 8 epoch, class weighting ile)
5. Test seti üzerinde tahmin (genel accuracy %81.41)

Test sonuçları:
- Genel accuracy: %81.41
- NORMAL recall: %53.42 (125/234)
- PNEUMONIA recall: %98.21 (383/390)

Modelimiz dengesiz veri (PNEUMONIA train'de NORMAL'in 3 katı) nedeniyle PNEUMONIA'ya eğilimli. Bu durumu sunumda "tıbbi bağlamda yüksek sensitivity tercih edilir" şeklinde hikayeleştireceğiz.

Eğitilmiş model `trainedNet` değişkeninde, test tahminleri ise `YPred`, `YTrue`, `scores` değişkenlerinde mevcut (workspace'te yüklü).

Şimdi yapacaklarım:
1. Confusion Matrix oluşturma ve görselleştirme
2. Performans metrikleri (Accuracy, Precision, Recall, F1-score, Specificity)
3. ROC eğrisi ve AUC
4. Doğru/yanlış sınıflandırılmış örnek görüntüleri görselleştirme
5. Grad-CAM ile modelin baktığı bölgeleri ısı haritası olarak gösterme
6. Sonuçların tartışılması ve sınırlılıklar

MATLAB'i az biliyorum ama yapabilirim. Bana hücre hücre, markdown başlıkları + kod + yorum şeklinde ilerlet. Her adımda kod ver, ben çalıştırayım, çıktıyı atayım, sen yorum yaz, sonraki adıma geçelim.

İlk olarak Confusion Matrix ile başlayalım.
```

---

## Push İşlemi (Çalışman Bittikten Sonra)

Yaptığın değişiklikleri GitHub'a göndermek için Git Bash'te:

```bash
git add pneumonia_classification.mlx
git status
git commit -m "feat: add evaluation, metrics and grad-cam visualization"
git push
```

`git status` komutu hangi dosyaların değiştiğini gösterir. `commit -m` içindeki mesajı yaptığın işe göre değiştirebilirsin. `push` işlemi GitHub'a yükler.

**Önemli:** `data/` klasörü, `*.mat` dosyaları gibi büyük dosyalar `.gitignore`'da olduğu için otomatik olarak GitHub'a yüklenmez. Sadece kod ve markdown güncellemeleri push edilir.

---

## Sorun Yaşarsan

- MATLAB hata veriyorsa, hatanın ekran görüntüsünü Ferit'e ya da Claude'a at
- Git komutları takılırsa Ferit'e sor
- Drive linkinden indirme problemi olursa Ferit'le iletişime geç