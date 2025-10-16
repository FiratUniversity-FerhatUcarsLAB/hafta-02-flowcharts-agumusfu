START

  Kullanıcıdan T.C. Kimlik No ve şifre iste
  GİRİŞ_BİLGİLERİ_AL()

  DOĞRULA(GİRİŞ_BİLGİLERİ)
  IF doğrulama başarısız THEN
    "Hatalı bilgi." mesajı göster
    END
  ELSE
    POLİKLİNİK_LİSTESİNİ_GÖSTER()
    Kullanıcıdan poliklinik seçmesini iste
    SEÇİLEN_POLİKLİNİK = Kullanıcının seçimi

    O poliklinikteki DOKTOR_LİSTESİNİ_GÖSTER()
    Kullanıcıdan doktor seçmesini iste
    SEÇİLEN_DOKTOR = Kullanıcının seçimi

    SEÇİLEN_DOKTOR için UYGUN_RANDEVU_TARİHLERİNİ_GETİR()
    Kullanıcıya uygun tarihleri göster
    Kullanıcıdan tarih seçmesini iste
    SEÇİLEN_TARİH = Kullanıcının seçimi

    SEÇİLEN_TARİH için UYGUN_RANDEVU_SAATLERİNİ_GETİR()
    Kullanıcıya uygun saatleri göster
    Kullanıcıdan saat seçmesini iste
    SEÇİLEN_SAAT = Kullanıcının seçimi

    RANDEVU_BİLGİLERİ = (Hasta Bilgisi, SEÇİLEN_POLİKLİNİK, SEÇİLEN_DOKTOR, SEÇİLEN_TARİH, SEÇİLEN_SAAT)
    Kullanıcıya randevu bilgilerini onaya sun
    
    IF Kullanıcı ONAYLARSA THEN
      RANDEVUYU_KAYDET(RANDEVU_BİLGİLERİ)
      Veritabanında ilgili saat dilimini "dolu" olarak işaretle
      "Randevunuz başarıyla oluşturulmuştur." mesajı göster
      SMS veya E-posta ile bilgilendirme yap
    ELSE
      "İşlem iptal edildi." mesajı göster
    END IF
  END IF

END
