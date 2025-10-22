
Bu proje, **Retrieval-Augmented Generation (RAG)** mimarisi kullanılarak geliştirilmiş bir **bilgi tabanlı akıllı ChatBot** sistemidir.  
Model, genel bilgilerin ötesine geçerek belirli bir veri kaynağına dayanarak **doğru, güvenilir ve kaynak temelli yanıtlar** üretmeyi amaçlar.  
Proje, büyük dil modellerinin (LLM) halüsinasyon problemini azaltmayı hedefler.

PROJENİN AMACI  

Büyük Dil Modelleri (LLM), genel bilgi üretiminde oldukça başarılıdır. Ancak:
- Spesifik kurum içi veriler,
- Güncel bilgiler,
- Özel dokümantasyonlar söz konusu olduğunda yanlış veya uydurma cevaplar verebilir.

Bu projede bu problem, **RAG (Retrieval-Augmented Generation)** mimarisiyle çözülmüştür.  
Kısaca:  
- **Retrieve (Çek):** Kullanıcı sorgusu vektör veri tabanına gönderilir.  
- **Augment (Zenginleştir):** En alakalı bilgiler çekilerek modele bağlam olarak eklenir.  
- **Generate (Üret):** Model sadece bu bağlamı kullanarak nihai cevabı üretir.  

---

## ⚙️ Teknik Yapı ve Kullanılan Teknolojiler

| Bileşen | Teknoloji | Açıklama |
|----------|------------|----------|
| **Ana Mimari** | RAG (Retrieval-Augmented Generation) | Doğru ve bağlama dayalı cevap üretimi sağlar. |
| **Dil Modeli (LLM)** | TinyLlama-1.1B-Chat-v1.0 | Sonuçların doğal dilde oluşturulması. |
| **Embedding Modeli** | all-MiniLM-L6-v2 | Metinleri yüksek boyutlu vektör uzayına dönüştürür. |
| **Vektör Veri Tabanı** | FAISS (Facebook AI Similarity Search) | Bilgi parçalarının hızlı aranmasını sağlar. |
| **Geliştirme Ortamı** | Python / Transformers | Model yönetimi ve pipeline işlemleri. |
| **Kullanıcı Arayüzü** | Gradio | Kullanıcı dostu web tabanlı test arayüzü. |

---

## OPTİMİZASYONLAR

### 1. Performans & Bellek
- **GPU Kullanımı:** CUDA destekli GPU’larda çalışacak şekilde optimize edildi.  
- **8-bit Quantization:** TinyLlama modeli, VRAM kullanımını %50 azaltan `load_in_8bit=True` parametresiyle yüklendi.  

### 2. Prompt Mühendisliği
- Model yalnızca sağlanan bağlamı kullanacak şekilde yönlendirildi.  
- Uygun bilgi yoksa sabit yanıt döner:  
  > “Elimdeki kaynaklarda bu bilgi bulunmamaktadır.”
- **Temperature:** 0.1 olarak ayarlandı — deterministik ve güvenilir yanıtlar için.

### 3. Veri Parçalama (Chunking)
- **chunk_size:** 500  
- **chunk_overlap:** 100  
Bu değerler, hem anlam bütünlüğünü korur hem de FAISS arama isabetini artırır.

---

## 🚀 Kurulum ve Çalıştırma

### 🔧 Gereksinimler
- Python 3.8+
- CUDA destekli NVIDIA GPU (T4 veya üzeri önerilir)

💡 “Gerçek zeka, yalnızca bilgiye erişmek değil, onu doğru bağlamda kullanabilmektir.”
PROJEYE ERİŞİM
---GOOGLE COLAB----
https://colab.research.google.com/drive/1Q1SeLxRCoGAEt14iB2VGPauU3RSyd3TN?usp=sharing
----KAGGLE------
https://www.kaggle.com/code/korkut61/chatbot?scriptVersionId=270074867
