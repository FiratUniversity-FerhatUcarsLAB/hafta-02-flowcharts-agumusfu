START

  Kullanıcıdan kartı al
  KART_OKU()

  IF kart geçerli DEĞİLSE THEN
    "Geçersiz Kart" mesajı göster
    Kartı iade et
    END
  ELSE
    Kullanıcıdan şifre iste
    ŞİFRE_GİR()
    
    DENEME_SAYISI = 1
    WHILE (DENEME_SAYISI < 3 AND ŞİFRE_DOĞRU DEĞİLSE)
      IF girilen şifre DOĞRU ISE THEN
        ŞİFRE_DOĞRU = EVET
      ELSE
        "Hatalı Şifre" mesajı göster
        DENEME_SAYISI = DENEME_SAYISI + 1
        Kullanıcıdan tekrar şifre iste
      END IF
    END WHILE

    IF ŞİFRE_DOĞRU DEĞİLSE THEN
      "Şifre 3 kez hatalı girildi. Kartınıza el konulmuştur." mesajı göster
      Karta el koy
      END
    ELSE
      İŞLEM_MENÜSÜNÜ_GÖSTER()
      Kullanıcıdan işlem seçmesini iste (Para Çekme)
      
      IF seçilen işlem == "Para Çekme" THEN
        Kullanıcıdan çekilecek tutarı iste
        TUTAR_GİR()

        HESAP_BAKİYESİ = Veritabanından bakiye sorgula
        
        IF girilen tutar <= HESAP_BAKİYESİ AND girilen tutar > 0 THEN
          YENİ_BAKİYE = HESAP_BAKİYESİ - girilen tutar
          Veritabanında bakiyeyi güncelle
          Parayı hazırlama bölmesine gönder
          Kullanıcıya parayı ver
          Kullanıcıya kartı iade et
          "İşlem tamamlandı." mesajı göster
        ELSE
          "Yetersiz Bakiye" veya "Geçersiz Tutar" mesajı göster
          Kullanıcıya kartı iade et
        END IF
      ELSE
        Diğer işlemleri yap (Örn: Bakiye Sorgulama)
        Kullanıcıya kartı iade et
      END IF
    END IF
  END IF
END
