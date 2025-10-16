START

  SİSTEM_DURUMU = "Devre Dışı"

  WHILE TRUE
    Kullanıcıdan komut bekle (Panel veya Mobil Uygulama)
    
    IF gelen komut == "Sistemi Kur" THEN
      SİSTEM_DURUMU = "Kurulu"
      "Sistem kuruldu." mesajı ver
    ELSE IF gelen komut == "Devre Dışı Bırak" AND girilen şifre DOĞRU ISE THEN
      SİSTEM_DURUMU = "Devre Dışı"
      "Sistem devre dışı bırakıldı." mesajı ver
      ALARM_DURUMU = "Kapalı"
    END IF
    
    IF SİSTEM_DURUMU == "Kurulu" THEN
      SENSÖRLERİ_KONTROL_ET()
      
      IF Hareket Sensörü tetiklendi OR Kapı/Pencere Sensörü tetiklendi THEN
        ALARM_DURUMU = "Aktif"
        Yüksek sesli sireni çal
        Işıkları yakıp söndür
        
        EV_SAHİBİNE_BİLDİRİM_GÖNDER("Tehlike algılandı!")
        GÜVENLİK_MERKEZİNE_SİNYAL_GÖNDER()
        
        İlgili kameradan video kaydı başlat
        Kaydı buluta yükle
      END IF
    END IF
    
    Bir süre bekle (örn: 1 saniye)
  END WHILE

END
