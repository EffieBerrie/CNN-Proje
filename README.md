# CNN Proje
Çanta ve cüzdan sınıflandırması

👜👛 Çanta / Cüzdan Görüntü Sınıflandırma Projesi

Bu projede, iki sınıflı (çanta ve cüzdan) bir görüntü veri seti üzerinde farklı derin öğrenme yaklaşımlarının performansları karşılaştırılmıştır. Amaç; transfer learning, custom CNN (baseline) ve iyileştirilmiş custom CNN yaklaşımlarının doğruluk ve genelleme kabiliyetlerini analiz etmektir.

📁 Veri Seti ve Ön İşleme

Sınıflar: canta, cuzdan


Veri seti üçe ayrılmıştır:

Train

Validation

Test


Tüm görüntüler 128×128 piksel boyutuna yeniden ölçeklendirilmiştir.

Test verileri eğitim sürecine kesinlikle dahil edilmemiştir.

Model 2 ve Model 3’te pikseller [0,1] aralığına normalize edilmiştir.

Model 1’de VGG16’ya uygun olacak şekilde preprocess_input kullanılmıştır.

🧠 Model 1 – Transfer Learning (VGG16)

🔹 Model Tanımı

Model 1’de, ImageNet veri seti üzerinde önceden eğitilmiş VGG16 mimarisi kullanılmıştır. Taban model dondurulmuş, yalnızca üst sınıflandırıcı katmanlar eğitilmiştir.

🔹 Mimari

VGG16 (pretrained, frozen)

Flatten

Dense (256, ReLU)

Dropout (0.3)

Dense (Softmax)


🔹 Özellikler

Transfer Learning yaklaşımı

Küçük veri setlerinde hızlı ve stabil öğrenme

ImageNet benzerliği avantajı

🔹 Sonuç

Test Accuracy: %90.90

Bu model, güçlü bir başlangıç (baseline) sağlar ancak önceden eğitilmiş bir mimariye bağımlıdır.

🧠 Model 2 – Geliştirilmiş Custom CNN (Baseline)

🔹 Model Tanımı

Model 2, sıfırdan tasarlanmış, Batch Normalization ve veri artırımı içeren bir custom CNN mimarisidir. Amaç, transfer learning kullanılmadan elde edilebilecek temel performansı ölçmektir.

🔹 Mimari

Conv(32) → BatchNorm → ReLU → MaxPool

Conv(64) → BatchNorm → ReLU → MaxPool

Conv(128) → BatchNorm → ReLU → MaxPool

Conv(256) → BatchNorm → ReLU → MaxPool

Global Average Pooling

Dense (256)

Dropout (0.5)

Softmax

🔹 Özellikler

Transfer learning yok

Orta düzey veri artırımı

Daha derin ama temkinli yapı

🔹 Sonuç

Test Accuracy: %63.64

Bu sonuç, Model 2’nin baseline custom CNN olarak görevini başarıyla yerine getirdiğini göstermektedir.

🧠 Model 3 – İyileştirilmiş Custom CNN (Final Model)

🔹 Model Tanımı

Model 3, Model 2’ye kıyasla daha sade, daha dengeli ve genelleme kabiliyeti yüksek olacak şekilde tasarlanmıştır. Amaç, gereksiz karmaşıklığı azaltarak performansı artırmaktır.

🔹 Temel Farklar

Daha az agresif veri artırımı

Daha küçük batch size

Daha düşük öğrenme oranı

Batch Normalization yerine mimari sadelik

🔹 Mimari

Conv(32) → MaxPool

Conv(64) → MaxPool

Conv(128) → MaxPool

Flatten

Dense (128)

Softmax

🔹 Sonuç

Test Accuracy: %90.91

✅ Sonuç

Model 3’ün final versiyonu, önceki tüm Model 3 denemelerine kıyasla daha yüksek doğruluk elde etmiş ve yapılan mimari/hiperparametre optimizasyonlarının etkisini net biçimde ortaya koymuştur.

Bu durum, deneysel yaklaşımın doğru şekilde ilerlediğini ve Model 3’ün beklenen performans artışını sağladığını göstermektedir.


Aşağıda yer alan görsellerde deney durumları ve test sonuçları listelenmiştir.

<img width="1606" height="156" alt="image" src="https://github.com/user-attachments/assets/cbd2c7e1-5799-48cb-9cce-3de919dab6bd" />


<img width="770" height="107" alt="image" src="https://github.com/user-attachments/assets/19b4d7e0-ca7f-4c86-bbd7-ad28c38a8bbe" />

