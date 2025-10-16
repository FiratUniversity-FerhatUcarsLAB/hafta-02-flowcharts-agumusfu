START

  Öğrenci No ve şifre iste
  GİRİŞ_YAP()
  
  IF giriş başarısız THEN
    "Hatalı bilgi." mesajı göster
    END
  ELSE
    ÖĞRENCİ_BİLGİLERİ = Veritabanından al (Bölüm, Sınıf, Kredi Limiti)
    AÇILAN_DERSLER_LİSTESİ = Veritabanından al
    
    Öğrenciye açılan dersleri göster
    
    SEÇİLEN_DERSLER = Boş liste
    TOPLAM_KREDİ = 0
    
    LOOP UNTIL (Öğrenci "Kaydı Tamamla" butonuna basar)
      Öğrenci bir ders seçer
      SEÇİLEN_DERS = Seçilen dersin bilgileri (Kredi, Kontenjan, Ön koşul)
      
      ÇAKIŞMA_VAR_MI = SEÇİLEN_DERS'in programı SEÇİLEN_DERSLER listesindekilerle çakışıyor mu?
      KREDİ_AŞILDI_MI = (TOPLAM_KREDİ + SEÇİLEN_DERS.Kredi) > Kredi Limiti mi?
      ÖNKOŞUL_SAĞLANDI_MI = Öğrenci dersin ön koşulunu almış mı?
      
      IF ÇAKIŞMA_VAR_MI == HAYIR AND KREDİ_AŞILDI_MI == HAYIR AND ÖNKOŞUL_SAĞLANDI_MI == EVET THEN
        SEÇİLEN_DERSLER listesine ekle
        TOPLAM_KREDİ = TOPLAM_KREDİ + SEÇİLEN_DERS.Kredi
        "Ders başarıyla eklendi." mesajı göster
      ELSE
        Hata mesajı göster (örn: "Ders çakışması var.", "Kredi limitini aştınız.")
      END IF
    END LOOP
    
    Seçilen ders listesini öğrenciye göster
    IF öğrenci ONAYLARSA THEN
      DERS_KAYDINI_DANIŞMAN_ONAYINA_GÖNDER()
      "Ders kaydınız danışman onayına gönderilmiştir." mesajı göster
    ELSE
      İşlemi iptal et
    END IF
  END IF
  
END
