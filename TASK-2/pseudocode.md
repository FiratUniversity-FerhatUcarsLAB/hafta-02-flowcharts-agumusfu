START

  SEPET = Boş bir liste/dizi oluştur

  Kullanıcı ürün sayfalarını gezer
  LOOP UNTIL (Kullanıcı "Ödeme Yap" butonuna basar)
    Kullanıcı bir ürün seçer ve "Sepete Ekle" butonuna basar
    SEÇİLEN_ÜRÜN = Kullanıcının seçtiği ürün bilgisi (ID, Fiyat, Adet)
    
    ÜRÜN_SEPTE_VAR_MI = SEPET içinde SEÇİLEN_ÜRÜN.ID ara
    
    IF ÜRÜN_SEPTE_VAR_MI == EVET THEN
      SEPET'teki ilgili ürünün Adet'ini bir artır
    ELSE
      SEÇİLEN_ÜRÜN'ü SEPET'e ekle
    END IF
    
    Kullanıcıya "Sepeti Görüntüle" seçeneği sun
    IF Kullanıcı "Sepeti Görüntüle" seçerse THEN
      SEPETTEKİ_ÜRÜNLERİ_LİSTELE()
      TOPLAM_TUTAR = 0
      FOR EACH ürün IN SEPET
        ÜRÜN_TUTARI = Ürün.Fiyat * Ürün.Adet
        TOPLAM_TUTAR = TOPLAM_TUTAR + ÜRÜN_TUTARI
      END FOR
      TOPLAM_TUTARI_GÖSTER()
      
      Kullanıcıya "Ürün Miktarını Güncelle" veya "Ürünü Sil" seçeneği sun
      IF Kullanıcı işlem yaparsa THEN
        İlgili ürünü SEPET'ten güncelle veya sil
      END IF
    END IF
  END LOOP
  
  ÖDEME_SAYFASINA_YÖNLENDİR(SEPET, TOPLAM_TUTAR)

END
