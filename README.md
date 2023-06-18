# Anonim-X

### Nasıl Kullanılır:

1. https://glitch.com adresine gidin ve kaydolun.
2. Yeni bir proje oluşturun ve "Git Repo'dan Klonla" seçeneğini seçin.
3. Aşağıdaki URL'yi kopyalayıp yapıştırın: https://github.com/aysegulmnk/Anonim-X.git
4. "Tamam" butonuna basın ve yüklemenin tamamlanmasını bekleyin.
5. Sol üst köşede "Göster"e tıklayın ve "Yeni Bir Pencerede" seçeneğini seçin.

#### Otomatik olarak aç:
1. https://glitch.com adresine gidin, kaydolun ve oturum açın.
2. https://glitch.com/edit/#!/remix/clone-from-repo?REPO_URL=https://github.com/aysegulmnk/Anonim-X adresini açın.
3. Sol üst köşedeki "Show" üzerine tıklayın ve "Yeni Bir Pencerede Aç" seçeneğini seçin.



#### Ek Notlar:

Eğer çalışmazsa, proje yüklendikten sonra ekranın sol tarafında "package.json" dosyasını arayın ve üzerine tıklayın. Ardından "Paket Ekle" düğmesine tıklayın ve karşınıza çıkan paketlerden herhangi birini indirmek için üzerlerine tıklayın. Eğer hala çalışmazsa, web sitesinin alt kısmında listelenen sosyal medya profillerimden biri aracılığıyla bana ulaşabilirsiniz.

Unutmayın, Glitch etkinliğin olmaması durumunda sunucunuzu otomatik olarak 30 dakika sonra kapatır.

Mesajlar, RSA-2048/3072/4096 (hangisini seçerseniz ona bağlı olarak) kullanılarak şifrelenir, bu yüzden karakter sınırlaması olabilir. Anahtar boyutu ne kadar büyükse, şifreleme o kadar güçlü olur (ancak sohbet uygulaması daha yavaş olur). Gelecekte, her mesajı AES ve rastgele bir anahtar kullanarak şifreleyebilirim, ardından RSA ile AES anahtarını şifreleyerek herhangi bir sınırlamayı aşabilirim, tamamen resimlerin nasıl şifrelendiği gibi.

Çoğu tarayıcının her web sitesi için 5 MB yerel depolama sınırlaması vardır. Depolama alanı dolarsa, yeni mesajlar ve konuşmalar kaydedilmez. Ayarlar paneli veya sohbet sayfası üzerinden durumu kontrol edebilirsiniz.

### Bu ne işe yarar?

Bu, kaydedilmeyen, kendi barındıran, açık kaynaklı, uçtan uca şifreli bir sohbet uygulamasıdır. Temel olarak, bir konuşma oluşturduğunuzda, tarayıcınızda yerel olarak bir özel ve genel anahtar çifti oluşturulur. Özel anahtar da dahil olmak üzere hiç kimse (sunucu dahil) özel anahtarın ne olduğunu bilmez. X:/Anonymous kullanarak diğer kişiye mesaj gönderdiğinizde, mesaj RSA kullanılarak şifrelenir. Konuşmalar da yerel olarak depolanır, bu nedenle sunucu tasarım gereği sizinle ilgili hiçbir bilgi kaydetmez. Yukarıda bahsettiğim Glitch web sitesi, uygulamayı barındırmak için kullanılsa bile, IP adreslerini ve benzer bilgileri saklar, ancak asla mesajlarınızın düz metin kopyasını elde etmezler. Herhangi bir aşamada özel anahtarınızı da almazlar. Bu nedenle, sunucu aslında iki kişi arasında gerçekten ne söylendiğini hiçbir şekilde bilmez ve kendi barındırmasından dolayı iletişim güvenliğinizi tehlikeye atabilecek herhangi bir zararlı kod veya şeyin olmadığını kesin olarak bilebilirsiniz.

### Dosya göderebilir miyim?

Evet, ancak şu anda yalnızca resimleri gönderebilirsiniz. İşleyiş şekli şu şekildedir: Bir resim seçersiniz, tarayıcınızda Base64'e dönüştürülür, rastgele bir dize oluşturulur ve bu dize AES kullanılarak Base64 dizesini şifrelemek için bir anahtar olarak kullanılır. Daha sonra anahtar, diğer kişinin genel anahtarı kullanılarak şifrelenir ve hem AES şifrelenmiş dize hem de RSA şifrelenmiş dize sunucuya gönderilir ve diğer kullanıcıya iletilir. Diğer kullanıcı daha sonra özel anahtarını kullanarak AES anahtarını çözer, anahtarı kullanarak dizeyi çözer ve sonunda resmi temsil eden Base64 dizesini elde eder. Dolayısıyla süreç boyunca sunucu görüntüyü göremez. Görüntü hiçbir yerde, hatta yerel depolamada bile saklanmaz (zaten çok büyük olur ve kullanıcıların yerel depolama alanı sınırlarını artırmalarını gerektirir).

### Buna neden ihtiyacım olabilir?

Hemen hemen her sosyal medya platformu bir sohbet özelliğine sahip olsa da, hepsi sohbetlerinizi okuyabilecek şekilde saklar. Bu büyük bir gizlilik ihlalidir. Bir kişiyle sadece bir kişiyle bir sırrı paylaşmak isterseniz, konuşmalarınıza potansiyel olarak yüzlerce kişinin erişimi olmadığını bilmek daha iyi hissettirmez mi?

### How does it work?

Haydi, birbirleriyle konuşmak isteyen ancak konuştukları şeyin mutlak bir sır olarak kalması gereken iki kişiden bahsedelim. Onları Ayşe ve Fatma olarak adlandıralım. Ayşe, Anonim-X kullanarak anonim bir konuşma oluşturur. Tarayıcısında, tamamen istemci tarafında, kendisi için bir genel anahtar ve özel anahtar oluşturulur. Ayşe, genel anahtarını sunucuya gönderir ve kendisi için bir anonim kimlik oluşturulur. Konuşmanın oluşturulduğu zaman, son olarak ne zaman değiştirildiği, Ayşe'nin anonim kimliği ve genel anahtarı içeren bir dosya sunucuda oluşturulur. Ayrıca bir konuşma kimliği de oluşturulur ve Ayşe sohbet sayfasına yönlendirilir. Şimdi Fatma'nın katılması için bir bağlantı göndermek için bir URL paylaşarak Fatma'ya bir link gönderebilir. Fatma bağlantıya tıklar ve onun için (hala istemci tarafında) bir özel ve genel anahtar çifti oluşturulur, bir anonim kimlik verilir ve sohbet sayfasına erişim sağlanır. Ayşe ve Fatma'nın özel anahtarları sunucu tarafından değil, tarayıcının yerel depolamasında saklanır. Birbirlerine mesaj gönderdiklerinde, mesajlarını karşıdaki kişinin genel anahtarıyla şifrelerler. Şifrelenmiş mesaj sunucuya gönderilir ve diğer kişiye iletilir, ardından karşıdaki kişi, özel anahtarıyla yerel olarak istemci tarafında şifrelemeyi çözer. Sunucunun hiçbir aşamada özel anahtarlara veya düz metin verilere erişimi yoktur. Gönderilen ve alınan mesajlar da tarayıcının yerel depolamasında saklanır. Dezavantajı, kullanıcılardan birinin yerel depolama kayıtlarını değiştirerek ve diğer kişinin söylemediği bir şeymiş gibi görünmesini sağlayarak bir mesajın orijinal içeriğini gerçekten kanıtlayabilecek bir yol olmamasıdır. Ancak, verilerinizi satmaktan büyük kazanç sağlayacak bir şirkete mi yoksa potansiyel olarak bir arkadaş olan tek bir kişiye mi güvenmek istersiniz?
