# Çalış

 1. sw_1 tiklaninca kirmizi ledi yak. Tiklamadan sonra bir miktar bekle ki arklari engellemis ol.
 2. sw_1'e 5 kez tıklanınca kırmızı ledi yak.
 3. sw_2'ye 3 kez tıklanınca mavi ledi yak. sw_2'nin calıştığından emin ol. Devam...
 4. 2. ve 3. adımı birleştir.
 5. sw_1 den bir ledi kaç kez yakacağımızı belirleyeceğiz. sw_2 ise kırmızı ledin yanıp sönmesini başlatacaktır. Yanma sönme aralığı delay komutunu kullanınız. Olay: sw_1 ile ledin kaç kez yakıp söndürüleceği girecek- bir değişkende kaç kez yakılacağını tutunuz. sw_2'ye basıldığı anda değişkenin miktarı kadar bir döngüde yanma sönme olayını yapınız. Örnek: sw_1 17 kez basmışsak, sw_2 ye basıldığı anda 17 kez ledi yakıp söndürünüz.
 6. 5. adımda yanıp sönme olayını fonksiyona atınız. Şablon :
		 ``` 
		 void ledxkadaryaksondur(int x){
			 for (kackez){
					yak
					bekle
					sondur
					bekle
			}
		}
		```
 7. Bir ledin yanip sonme zamanlarini arttirip azaltacak kodu yaziniz. sw_1 tiklaninca yanma suresi artsin, sw_2 tiklaninca da azalsin.
 
