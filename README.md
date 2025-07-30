                                     ┌────────────────────────┐
                                     │   1. Başlangıç         │
                                     │   (Abone hizmete       │
                                     │    ilk bağlandığında)  │
                                     └────────┬───────────────┘
                                              │
                                              ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. Abone & Çevresel Veri Toplama                                       │
│    • Radyo koşulları (RSRP, RSRQ, SINR, kapsama haritası)             │
│    • Trafik yükü (PRB kullanımı, hücre kapasitesi)                    │
│    • QoE metrikleri (hız, gecikme, paket kaybı)                       │
│    • Abone uygulama profili (OTT türü, bant genişliği, süre)          │
│    • Konum, hareketlilik, cihaz yetenekleri                           │
└────────────────────────┬───────────────────────────────────────────────┘
                         │
                         ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. Şebeke Analiz Ajanı (Agentic-AI Modül #1)                           │
│    • Verileri sürekli analiz eder                                     │
│    • “Mevcut slice QoE’yi karşılıyor mu?” kararını verir              │
└──────────────┬─────────────────────────────────────────────────────────┘
               │
      Hayır ◄──┴──► Evet
               │                │
               │                └──────────────┐
               ▼                               │
┌────────────────────────────┐                │
│ 4. Deneyim İyileştirme     │                │
│    Ayar Belirleme Ajanı    │                │
│    (Agentic-AI Modül #2)   │                │
│    • Yeni slice profili    │                │
│      (QoS, QoE, kapasite)  │                │
│    • Kaynak atama          │                │
│      senaryoları           │                │
└──────────┬─────────────────┘                │
           │                                  │
           ▼                                  │
┌────────────────────────────┐                │
│ 5. Aboneye Teklif Sunumu   │                │
│    (GUI/APP/SMS)           │                │
│    • “Daha iyi deneyim     │                │
│      için Premium slice    │                │
│      teklifi”              │                │
└────┬───────────┬───────────┘                │
     │           │                          (izleme)
     │           │                            ▲
     │           └─► Abone Reddeder ──────────┘
     │                   (Mevcut slice korunur, 3’e dön)
     ▼
  Abone Kabul Eder
     │
     ▼
┌────────────────────────────┐
│ 6. Aboneye Özel Dinamik    │
│    Slice Ataması           │
│    (SMF/AMF/UPF + RIC)     │
│    • Süreli / kalıcı flag  │
└──────────┬─────────────────┘
           │
           ▼
┌────────────────────────────┐
│ 7. Servis Kalitesi Ölçüm & │
│    Takip Ajanı             │
│    (Agentic-AI Modül #3)   │
│    • KPI’lar > threshold?  │
└────┬───────────┬───────────┘
     │           │
     │ Hayır     │ Evet
     │           ▼
     │   ┌─────────────────────────┐
     │   │ 8. Slice Güncelleme /   │
     │   │    Yeni Teklif          │
     │   └────────┬────────────────┘
     │            │
     └────────────┴──► 3 (Şebeke Analiz) döngüsü



                                     ┌────────────────────────┐
                                     │      1. Başlangıç      │
                                     │  (Abone hizmete ilk    │
                                     │   bağlandığında)       │
                                     └────────┬───────────────┘
                                              │
                                              ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. Abone & Çevresel Veri Toplama                                       │
│    • Radyo koşulları, trafik, QoE metrikleri                           │
│    • Konum, cihaz yetenekleri                                          │
└──────────────┬─────────────────────────────────────────────────────────┘
               │
               ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2A. Abone Uygulama Davranış Analizi                                    │
│    • Uygulama türleri, yoğun saatler, bant/SLA eğilimleri              │
│    • “Davranış profili” oluşturulur                                    │
└──────────────┬─────────────────────────────────────────────────────────┘
               │
               ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. Şebeke Analiz Ajanı                                                 │
│    • Veri + davranış profili birlikte değerlendirilir                  │
│    • “Mevcut slice QoE’yi karşılıyor mu?”                              │
└──────┬───────────────┬─────────────────────────────────────────────────┘
       │               │
   Hayır              Evet
       │               │
       ▼               │
┌────────────────────────────┐      │
│ 4. Deneyim İyileştirme     │      │
│    Ayar Belirleme Ajanı    │      │
│    • Yeni slice profili    │      │
│      (kapasite, QoS)       │      │
└──────┬───────────────┘      │
       ▼                       │
┌────────────────────────────┐ │
│ 4A. Davranış Odaklı        │ │
│    İyileştirme Teklifi     │ │
│    • Davranışa özel        │ │
│      parametreler          │ │
└──────┬───────────────┘ │
       │                 │
       ▼                 │
┌────────────────────────────┐
│ 5. Aboneye Teklif Sunumu   │
│    • “Davranışınıza özel   │
│      Premium slice”        │
└──────┬──────────┬───────────┘
       │          │
   Kabul          Red
       │          │
       ▼          │
┌────────────────────────────┐
│ 6. Aboneye Özel Dinamik    │
│    Slice Ataması           │
│    • Süreli / kalıcı       │
└──────┬─────────────────────┘
       ▼
┌────────────────────────────┐
│ 7. Servis Kalitesi Ölçüm & │
│    Takip Ajanı             │
│    • KPI’lar izlenir       │
└──────┬──────────┬───────────┘
       │          │
   Güncelle      Değil
       │          │
       └──────────┴──► 3 (Şebeke Analiz) döngüsü
