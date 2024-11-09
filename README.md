
Sınıf Bilgisi/Hiyerarşisi 

Program() 

“main()” üzerinden SettingsForm’u başlatır. 

 

SettingsForm(Form) 

Windows Forms kullanarak “SettingsForm.designer.cs” dosyası aracılığıyla bir form açar. 

startButton_Click() fonksiyonunu kullanarak formdan gelen nesnelerin (gridSize, mineNum ve playerName) kabul edilebilir olup olmadığına bakar, kabul ederse nesneleri “Oyun”a yollar ve “game.Run()” komutu ile oyunu resmen başlatır. 

  

Oyun (Game) 

Nesneler: 

Grafik ayarları ve ekran yönetimi için _graphics (GraphicsDeviceManager) ve _spriteBatch (SpriteBatch). 

Hücre  ve tahta boyutu (cellSize, gridSize), skor (score), hamle sayacı (tmove),mayın sayısı (mineNum), oyuncu ismi (playerName) ve oyun durumu (isGameOver, isScroll) ile ilgili değişkenler. 

Oyunun grid yapısını ve mayın konumlarını tutmak için grid, açılan hücreleri tutmak için revealed, işaretli hücreleri tutmak için flagged adlı iki boyutlu diziler. 

Texture2D türündeki oyun grafikleri (cellTexture, mineTexture, flagTexture, zeroTexture, background, scroll, numTextures) ve yazı fontu (font). 

Bayrak koyma ve hamle sayacı ile alakalı flagToggleDelay, gameStartTime, lastToggleTime zaman nesneleri. 

 

Constructor (Oyun) 

Oyun sınıfının konstrüktörü; grid boyutunu, mayın sayısını ve oyuncu ismini formdan doğru alır ve grid, açılan hücreler ve bayraklı hücreler için ikili dizileri oluşturur. 

Grafik ayarları yapılır ve ekran boyutları ayarlanır. 

 

Metodlar: 

Initialize() 

Oyunun başlatılması ve mayınların rastgele yerleştirilmesini sağlar. 

Skorlamada kullanılacak olan oyun içi zamanı başlatır. 

CountMines(int x, int y) 

Belirli bir hücreye komşu olan gridlere bakar ve “-1” değerini aldığı komşu sayısını yani mayın sayısını hesaplar. 

gameOver() 

IsGameOver bool’unu true yapar. 

revealed dizisiyle grid dizisini karşılaştırarak bayraklanmış mayın sayısını hesaplar, sonra bu sayıyı oyunda geçen zamana böler ve 1000 ile çarparak skoru bulur ve “SaveScore()” metodunu çalıştırır.  

SaveScore() 

“StreamWriter” kullanarak eğer yoksa scores.txt dosyasını yaratır. 

Oyuncu skorunu scores.txt dosyasına yazar. 

RevealCell(int x, int y) 

Gelen x ve y değerleri ekranın dışında, açılmış ya da bayraklanmış mı diye kontrol eder, yani gelen x,y sayılarını revealed ve flagged dizilerinde dener ve değilse işleme devam eder. 

Bir hücreyi açar yani revealed dizisinde “1” yapar ve hücre çevresindeki hücreler için kendini geri çağırır. 

LoadContent() 

MonoGame’in “Content.Load” fonksiyonunu kullanarak içerik ve grafik dosyalarını/texturelerini yükler (hücre, mayın, bayrak dokuları vb.). 

Update(GameTime gameTime) 

“Escape” tuşuna basılması durumunda oyunu kapatır. 

Eğer isGameOver “false” ise her sol tıklamada tıklana yerin x,y sini alır “cellSize”a böler ve “RevealCell” e gönderir. 

Parşomen Rectangle’ı nesnesine basılı tutuduğu sürece isScroll’u “true” yapar. 

Her sağ tıklamada tıklanan hücre açık değilse oranın flagged değerini “1” yapar yani bayraklar. 

Bayraklanmış mayın sayısı, mayın sayısına eşit olduğunda “gameOver()”’ı çağırır. 

Draw(GameTime gameTime) 

Oyun ekranını çizer, her bir gride/hücreye ikili dizilerden gelen bilgilere göre texture verir. 

isScroll “true” ise “ReadAllLines” ile scores.txt’i okur ve ekrana yazdırır. 

isGameOver “false” ise parşomeni ve hareket sayacını gösterir 

isGameOver “true” ise Final Skorunu, Toplam Hareketi ve yapımcının adı soyadını/numarasını ekrana yazar. 
