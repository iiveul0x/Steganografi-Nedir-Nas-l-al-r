# Steganografi Nedir?

> Bir yazarın masumca yazdığı yazı, bir grafikerın zaman harcayıp tasarladığı logo, bir müzisyenin oluşturduğu müzik içinde gizlenen, normal bir şekilde baktığımızda göremeyeceğimiz gizleme bilimine steganografi denir. Steganograflar için en uygun gizleme yeri medya yani ses, görüntüler, video vb. dosyalardır.

## Steganografi Nasıl Uygulanır, Araçların Kullanımı?

>Steghide, OpenStego gibi araçları kullanabiliriz veya ses dosyalarına bir şeyler gizlemek için Coagula programını kullanabiliriz. Bu programların yaptığı şeylerin benzerini yapan araçlar github’da bulunuyor.

•  WavSteg

•  LSBSteg

•  StegDetect

Bu araçlar ile de veri gizleyebilirsiniz. 


## Steghide

> Steghide aracı, bir görsele veri gizlememizi ve veriyi tekrar çıkartmamızı sağlar. Hemen kullanımına kısaca bakalım.

```
steghide embed -cf 1.jpg -ef 1.txt
Enter passphrase:
Re-Enter passphrase:
embedding “1.txt” in “1.jpg”… done
```
burada 1.jpg resmimin içine 1.txt içerisindeki metnimi yerleştirdim ve metnimi güvende tutmak için bir parola girdim. Şimdi bu gizli metni aynı araç ile çıkartalım.

```
steghide --extract -sf 1.jpg -p 1234
the file “1.txt” does already exist. overwrite ? (y/n) y
wrote extracted data to “1.txt”.
```

1.jpg resmimden gizli metnimi parolamı girdikten sonra 1.txt olarak bulunduğum konuma çıkarttı.

Eğer başkasının oluşturduğu ve parola ile koruduğu veriyi açmak istiyorsanız brute-force yolu ile çıkartabilirsiniz, bunun için bazı araçlar github’da bulunuyor.


## OpenStego

OpenStego da steghide ile aynı işlevleri görüyor fakat windows için sürümü de olduğu için daha kolay ve hızlı bir şekilde bilgileri gizleyebiliriz. OpenStego iki özellik sunuyor;

• **Veri Gizleme**: Bir fotoğrafa herhangi veriyi aynı steghide’de olduğu gibi gizleyebilir.

• **Filigran (beta)**: Görünmez imzalı filigran dosyaları oluşturabilir.

Kısaca veri gizleme ve filigranlama yapabiliyoruz.

[Web sitesine buradan ulaşabilirsiniz.](https://www.openstego.com)


## Coagula

Coagula ile ses dosyalarımızın içerisine veri girerek gizleyebiliriz. Programı açtığımızda bize bir fırça veriyor bu fırça ile yazımızı yazıp çıktımızı alıyoruz. Şimdi ufak bir uygulama yapalım.

Programı açıp, fırça ile yazınızı yazdığınızı varsayıyorum. Yazdıktan sonra aşağıdaki görselde gösterilen butona tıklıyoruz.

![gorsel](https://kernelblog.org/wp-content/uploads/2021/05/Coagula.png.webp)

Tıkladıktan sonra bir takım garip sesler duyacaksınız. Sonra **File > Save sound as** diyerek ses dosyamızı kaydediyoruz.

Kayıt ettikten sonra “KernelBlog” verimizi gizlemiş olduk.

Audacity programında ses dosyamızı açıyoruz.

Ses dosyamızı ekledikten sonra, ses dalgalarının sol tarafında dosya adımızın yazdığı yere tıklayıp, aşşağıdaki görselde olduğu gibi spektrogram yazan kısma tıklıyoruz. 

![gorsel2](https://kernelblog.org/wp-content/uploads/2021/05/Audacity_spektrogram.png.webp)

Tıkladıktan sonra aşağıdaki görselde olduğu gibi yazdığımız yazıyı görüyoruz.

![gorsel3](https://kernelblog.org/wp-content/uploads/2021/05/Audacity_spektrogram_kernelblog.png.webp)

[Coagula programını bu adresten indirebilirsiniz.](https://www.abc.se/~re/Coagula/Coagula.html)

## WavSteg, LSBSteg, StegDetect

Bu araçlar yukarıda belirttiğim gibi tek bir github reposunda bulunuyor. Kurulumları ve kullanımları github adreslerinde yeterince açık şekilde belirtilmiş ama ben yine de sizler için kısa ve öz şekilde anlatmaya çalışacağım.

Github’dan dosyalarını çekip, setup dosyasını çalıştıralım.

```
git clone https://github.com/ragibson/Steganography
cd Steganography
python3 setup.py install
```

Kurulum işlemlerimiz bitti şimdi bu 3 aracı basit şekilde kullanımını gösterelim.

## WavSteg

```
stegolsb wavsteg -h -i sesdosyam.wav -s gizlimetin.txt -o stegsescikti.wav -n 1
```

Burayı açıklamak gerekirse;

• stegolsb wavsteg: Yazarak stegolb’da wavsteg aracını kullanacağımızı belirtiyoruz.

• -h ve -i sesdosyam.wav: -h parametresi hide yani gizlemek için kullanıyoruz. -i ile dosyamızın yolunu belirtiyoruz.

• -s gizlimetin.txt: -s parametresi ile gizlenecek dosya yolunu belirtiyoruz.

• -o stegciktises.wav: burada ise -o ile verimizi gizledikten sonra çıktı yolunu belirtiyoruz.

## LSBSteg

LBSSteg kısa ve en öz şekilde bit steganografisini kullanıyor (PNG veya BMP).

```
stegolsb steglsb -h -i input_image.png -s input_file.zip -o steg.png -n 2 -c 1
```

Burada tek tek açıklama yapmayacağım wavsteg ile aynı mantık sayılır. Parametrelerine bakmak için github adresini inceleyebilirsiniz.

## StegDetect

StegDetect, görüntülerdeki steganografiyi tespit etmeye çalışır.

```
stegolsb stegdetect -i input_image.png -n 2
```

•  -i parametresi ile görüntümüzün yolunu giriyoruz.

•  -n parametresi ile LBS sayısını giriyoruz (varsayılan 2).

## StegCracker

Bonus olarak bunu da eklemek istedim. Bu araç ile görüntülere gizlenen ama parolası olan verileri açmak istediğimizde yani steghide ile bir görüntüye veri gömdük, bunun parolasını bilmediğimizi düşünürsek açmak için stegcracker aracını kullanabilirsiniz.

Eğer kali linux kullanıyorsanız aşağıdaki komut ile kurabilirsiniz.

```
sudo apt-get install stegcracker -y
```

Kullanımı gayet basit brute-force için bir wordlist olması yeterli.

```
sudo apt-get install stegcracker -y
```

Bu steganografi için güzel bir başlangıç olur diye düşünüyorum. Umarım işinize yarar. Bir sonraki yazımda görüşmek üzere.


> Yazar: [Emre Yılmaz](https://emreylmz.com) Kaynak: [kernelblog](https://kernelblog.org)


