TR & EN |

# ✈️ Sivil ve Askeri Uçak Tanıma Veri Seti

Bu veri seti, hem sivil hem de askeri uçakları içeren kapsamlı bir uçak tanıma veri setidir. Veri seti, farklı açılardan görüntüler içerir ve çeşitli uçak kategorilerini kapsar.

## 📁 Veri Seti Hakkında

Bu veri seti, uçak tanıma ve sınıflandırma modelleri geliştirmek için oluşturulmuştur. Veri seti, aşağıdaki kategorileri içermektedir:

- **Sivil Uçaklar**: Airbus ve Boeing aileleri dahil olmak üzere ticari yolcu uçakları
- **Askeri Uçaklar**: II. Dünya Savaşı'ndan modern savaş uçaklarına kadar çeşitli askeri uçaklar
- **İnsansız Hava Araçları (İHA'lar)**: MQ-9 Reaper, Global Hawk, Predator gibi askeri İHA'lar ve DJI Phantom gibi sivil İHA'lar
- **Eğitim Uçakları**: Cessna 172, Piper PA-28 gibi eğitim amaçlı kullanılan uçaklar

## 📊 Veri Seti İstatistikleri

- **Toplam Görüntü Sayısı**: 8,275
- **Kategoriler**:
  - Sivil Uçaklar: 680 görüntü (17 sınıf)
  - Askeri Uçaklar: 7,467 görüntü (30 sınıf)
  - İHA'lar: 87 görüntü (5 sınıf)
  - Eğitim Uçakları: 41 görüntü (3 sınıf)
- 📌 **Veri Seti Bölünmesi**:
  - Eğitim (Train): 5,777 görüntü
  - Test: 1,226 görüntü
  - Doğrulama (Validation): 1,272 görüntü

## 🗂️ Veri Seti Yapısı

Veri seti, aşağıdaki yapıda organize edilmiştir:

```
data/
├── final/
│   ├── train/
│   │   ├── civil/
│   │   │   ├── [uçak_modeli_1]/
│   │   │   ├── [uçak_modeli_2]/
│   │   │   └── ...
│   │   ├── military/
│   │   ├── uav/
│   │   └── training/
│   ├── test/
│   │   ├── civil/
│   │   ├── military/
│   │   ├── uav/
│   │   └── training/
│   └── validation/
│       ├── civil/
│       ├── military/
│       ├── uav/
│       └── training/
├── metadata/
│   ├── aircraft_metadata.json
│   ├── dataset_summary.json
│   ├── sample_images/
│   └── visualizations/
```

## Görüntü Özellikleri

- **Boyut**: Tüm görüntüler 224x224 piksel boyutuna standartlaştırılmıştır
- **Format**: RGB formatında JPEG görüntüler
- **Etiketleme**: Hiyerarşik etiketleme (kategori, üretici, model)

## 🖼️ Sınıf Dağılımı

### Sivil Uçaklar (17 sınıf)
- ATR 42, ATR 72
- Airbus A220, A318, A319, A320, A321, A330, A350, A380
- Boeing 737 NG, 737 MAX, 747, 767, 777, 777X, 787

### Askeri Uçaklar (30 sınıf)
- Avro Lancaster, Bell P-63 Kingcobra, Boeing B-17 Flying Fortress, Boeing B-29 Superfortress
- Boeing P-26 Peashooter, Brewster F2A Buffalo, Consolidated PBY Catalina
- Curtiss P-40 Warhawk, Douglas A-20 Havoc, Douglas C-47 Skytrain
- Douglas SBD Dauntless, Douglas TBD Devastator, Focke-Wulf Fw 190
- Grumman F6F Hellcat, Grumman F7F Tigercat, Grumman TBF Avenger
- Hawker Hurricane, Junkers Ju 87, Lockheed P-38 Lightning
- Messerschmitt Bf 109, Mitsubishi A6M Zero, North American P51 Mustang
- Northrop P-61 Black Widow, Republic P-43 Lancer, Republic P-47 Thunderbolt
- Seversky P-35, Supermarine Spitfire, Vought F4U Corsair
- Waco CG-4, de Havilland Mosquito

### İHA'lar (5 sınıf)
- MQ-9 Reaper, Global Hawk, Predator
- DJI Phantom, Bayraktar TB2

### Eğitim Uçakları (3 sınıf)
- Cessna 172, Piper PA-28, Diamond DA20

## Metadata

Veri seti, her uçak modeli için aşağıdaki metadata bilgilerini içerir:

- Üretici
- Tip
- İlk uçuş yılı
- Rol
- Boyutlar (uzunluk, kanat açıklığı, yükseklik)
- Maksimum hız
- Menzil
- Açıklama

## 🧠 Kullanım Alanları

Bu veri seti aşağıdaki alanlarda kullanılabilir:

1. **Makine Öğrenimi ve Bilgisayarlı Görü**:
   - Uçak tanıma ve sınıflandırma modelleri geliştirme
   - Transfer öğrenimi için ön eğitimli modeller oluşturma

2. **Havacılık Güvenliği**:
   - Havaalanı güvenlik sistemleri için uçak tanıma
   - Hava sahası izleme sistemleri

3. **Eğitim ve Araştırma**:
   - Havacılık öğrencileri için eğitim materyali
   - Uçak tasarımı ve aerodinamik araştırmaları

4. **Hobi ve Eğlence**:
   - Uçak spotterlar için referans
   - Havacılık meraklıları için tanıma uygulamaları

## Örnek Kullanım

### Python ile Görüntü Sınıflandırma Modeli Eğitimi

```python
import tensorflow as tf
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.layers import Dense, GlobalAveragePooling2D
from tensorflow.keras.models import Model

# Veri yolları
train_dir = 'data/final/train'
validation_dir = 'data/final/validation'
test_dir = 'data/final/test'

# Veri artırma ve ön işleme
train_datagen = ImageDataGenerator(
    rescale=1./255,
    rotation_range=20,
    width_shift_range=0.2,
    height_shift_range=0.2,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True,
    fill_mode='nearest'
)

validation_datagen = ImageDataGenerator(rescale=1./255)
test_datagen = ImageDataGenerator(rescale=1./255)

# Veri akışları oluşturma
train_generator = train_datagen.flow_from_directory(
    train_dir,
    target_size=(224, 224),
    batch_size=32,
    class_mode='categorical'
)

validation_generator = validation_datagen.flow_from_directory(
    validation_dir,
    target_size=(224, 224),
    batch_size=32,
    class_mode='categorical'
)

test_generator = test_datagen.flow_from_directory(
    test_dir,
    target_size=(224, 224),
    batch_size=32,
    class_mode='categorical'
)

# Transfer öğrenimi için temel model
base_model = MobileNetV2(weights='imagenet', include_top=False, input_shape=(224, 224, 3))

# Temel modeli donduralım
base_model.trainable = False

# Yeni sınıflandırma katmanları ekleyelim
x = base_model.output
x = GlobalAveragePooling2D()(x)
x = Dense(1024, activation='relu')(x)
predictions = Dense(train_generator.num_classes, activation='softmax')(x)

# Modeli oluşturalım
model = Model(inputs=base_model.input, outputs=predictions)

# Modeli derleyelim
model.compile(
    optimizer='adam',
    loss='categorical_crossentropy',
    metrics=['accuracy']
)

# Modeli eğitelim
history = model.fit(
    train_generator,
    steps_per_epoch=train_generator.samples // train_generator.batch_size,
    epochs=20,
    validation_data=validation_generator,
    validation_steps=validation_generator.samples // validation_generator.batch_size
)

# Modeli değerlendirelim
test_loss, test_acc = model.evaluate(test_generator)
print(f'Test accuracy: {test_acc:.4f}')

# Modeli kaydedelim
model.save('aircraft_classification_model.h5')
```

## Lisans Bilgileri

Bu veri seti, aşağıdaki kaynaklardan toplanan görüntülerden oluşturulmuştur:

1. FGVC Aircraft Dataset - Araştırma amaçlı kullanım
2. Iconic WWII Aircraft Images-Classification - CC0: Public Domain
3. Web'den toplanan açık kaynaklı görüntüler - CC BY 4.0

Bu veri seti, akademik ve araştırma amaçlı kullanım için serbestçe kullanılabilir. Ticari kullanım için lütfen orijinal görüntü kaynaklarının lisans koşullarını kontrol edin.

## Teşekkürler

Bu veri seti, aşağıdaki kaynakların katkılarıyla oluşturulmuştur:

- FGVC Aircraft Dataset (http://www.robots.ox.ac.uk/~vgg/data/fgvc-aircraft/)
- Kaggle'daki çeşitli havacılık veri setleri
- Wikimedia Commons ve diğer açık kaynaklı görüntü kaynakları

## İletişim

Bu veri seti hakkında sorularınız veya geri bildirimleriniz için lütfen iletişime geçin.

---

© 2025 Burak Kurt. Tüm hakları saklıdır.


-----


# ✈️ Civil and Military Aircraft Recognition Dataset

A high-quality image dataset for recognizing and classifying both **civil** and **military** aircraft from various perspectives.

---

## 📁 Dataset Overview

This dataset is designed for training machine learning models in aircraft recognition. It includes:

- **Civil Aircraft**: Airbus, Boeing, and more  
- **Military Aircraft**: WWII to modern combat aircraft  
- **UAVs (Drones)**: MQ-9 Reaper, Predator, DJI Phantom, Bayraktar TB2  
- **Trainer Aircraft**: Cessna 172, Piper PA-28, Diamond DA20  

---

## 📊 Dataset Statistics

| Category  | Images | Classes |
|-----------|--------|---------|
| Civil     | 680    | 17      |
| Military  | 7,467  | 30      |
| UAVs      | 87     | 5       |
| Trainer   | 41     | 3       |
| **Total** | 8,275  | 55      |

### 📌 Dataset Split

- Train: 5,777 images  
- Validation: 1,272 images  
- Test: 1,226 images  

---

## 🗂️ Directory Structure
data/
├── final/
│   ├── train/
│   │   ├── civil/
│   │   │   ├── [uçak_modeli_1]/
│   │   │   ├── [uçak_modeli_2]/
│   │   │   └── ...
│   │   ├── military/
│   │   ├── uav/
│   │   └── training/
│   ├── test/
│   │   ├── civil/
│   │   ├── military/
│   │   ├── uav/
│   │   └── training/
│   └── validation/
│       ├── civil/
│       ├── military/
│       ├── uav/
│       └── training/
├── metadata/
│   ├── aircraft_metadata.json
│   ├── dataset_summary.json
│   ├── sample_images/
│   └── visualizations/


## 🖼️ Image Specifications

- Size: **224x224 pixels**
- Format: **RGB JPEG**
- Labels: **Hierarchical (category → manufacturer → model)**

---

## 🧠 Example Usage (TensorFlow)

```python
from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.layers import Dense, GlobalAveragePooling2D
from tensorflow.keras.models import Model

base_model = MobileNetV2(weights='imagenet', include_top=False, input_shape=(224, 224, 3))
base_model.trainable = False

x = GlobalAveragePooling2D()(base_model.output)
x = Dense(1024, activation='relu')(x)
output = Dense(NUM_CLASSES, activation='softmax')(x)

model = Model(inputs=base_model.input, outputs=output)
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

history = model.fit(train_generator, validation_data=val_generator, epochs=20)

🔧 Possible Applications

    Aircraft recognition and detection

    Transfer learning / pretrained models

    Aviation security and monitoring systems

    Academic research in aviation and defense technologies

📜 License & Sources

Images were collected from the following public/open sources:

    FGVC Aircraft Dataset

    WWII Aircraft Archives (CC0)

    Web-scraped images (CC BY 4.0)

    📌 This dataset is free for academic and non-commercial research purposes.

🙏 Acknowledgements

Special thanks to:

    Oxford VGG Group

    Kaggle Contributors

    Wikimedia Commons

    Public Domain Aircraft Archives

📬 Contact
Burak Kurt
© 2025 Burak Kurt – All rights reserved.
