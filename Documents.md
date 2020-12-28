---


---

<h1 id="uni̇ty-dökümantasyonu">UNİTY DÖKÜMANTASYONU</h1>
<blockquote>
<h2 id="user-interface"><strong>USER INTERFACE</strong></h2>

## Skor Ekranının Hazırlanması
Skor işlemleri genellikle iki script kullanılarak yapılır. Bunlardan biri puan algoritmasını yazdığımız **puanManager** diğeri ise oyunumuzun skoru arttırmasını istediğimiz **gameManager** isimli scriptler olsun.

**puanManager :**

UI İŞLEMLERİ İÇİN UI KÜTÜPHANESİ EKLEMEMİZ GEREKMEKTEDİR !!!

    using UnityEngine.UI;

İlk olarak toplam puanımızı arttıracağımız ve yeri geldiğinde yazdıracağımız **toplamPuan** değişkenini, daha sonra her seferinde kaç puan arttırmak istediğimizi tuttuğumuz **puanArtisi** değişkenini ve en son da skorumuzu ****UI**' a** yansıtmamız için **Text** türünden bir **puanText** değişkenini tanımlıyoruz.

    int toplamPuan;
    int puanArtisi;
    
    [SerializeField]
    Text puanText;

Start fonksiyonumuzda başlangıç skorumuzu sıfır olarak tanımladıktan sonra bunu UI da yazdırıyoruz.

     void Start()
        {
            toplamPuan = 0;
            puanText.text = toplamPuan.ToString();
            
        }


Tanımladığımız void fonksiyonumuzu zamanı geldiğinde çağırarak skorumuzun artmasını sağlayacağız

    public void puanArttir()
        {
    
            toplamPuan = toplamPuan + 5;
            puanText.text = toplamPuan.ToString();
    
        }


**gameManager:**

**puanManager** scripttine erişebilmek için tanımlamamızı en üste yapıyoruz.

    PuanManager puanmanager;

Start fonksiyonumuzda tanımladığımız nesneye, scriptimize erişim iznini sağlıyoruz.

    void Start()
    {
    	puanmanager = Object.FindObjectOfType<PuanManager>();
    }
Geriye kalan tek şey istediğimiz yerde fonksiyonumuzu şu şekilde çağırmak olacak

     puanmanager.puanArttir();

</blockquote>
<h2 id="animasyon-ekleme">Animasyon Ekleme</h2>
<h3 id="dofadefloat-bitiş_değeri-float-zamanlama">DOFade(float bitiş_değeri, float zamanlama)</h3>
<p>Bu fonksiyonun temel amacı objelerin renklerindeki <strong>“A”</strong> değerini yani saydamlığını belirli bir süre zarfında değiştirmektir. En çok kullandığım objeler buton ve panellerdir.</p>
<p>Ben bu fonksiyonu oyunumun başlangıç menüsü açılırken butonların animasyonlu bir şekilde gelmesi için kullandım.</p>
<h4 id="kullanimi">KULLANIMI</h4>
<p>Assetstoredan <strong>DOTween (HOTween v2) Free</strong> eklentisini indirip projemize ekliyoruz.</p>
<p>Kullanacağımız classımıza <strong>using DG.Tweening</strong> şeklinde ekliyoruz.</p>
<p>Saydamlaştırmayı istediğimiz objemize(benim için buton) <strong>canvas group</strong> eklememiz gerekmektedir.</p>
<p>Kodlara geçmeden öncede butonlarımızda bulunan <strong>canvas grouptaki</strong>  <strong>alpha</strong>  değerini sıfır yapıyoruz.</p>
<p><strong>Örnek1:</strong></p>
<pre><code>[SerializeField]
 GameObject startBtn, exitBtn;
</code></pre>
<p>Butonlarımızın <strong>alpha</strong> değeri sıfırdı fonksiyonumuzun ilk parametresi <strong>alpha</strong> değerinin bitiş değerini ikinci parametresi ise bu işlemi yapacağı süreyi söylemektedir</p>
<pre><code>startBtn.GetComponent&lt;CanvasGroup&gt;().DOFade(1, 0.8f);

exitBtn.GetComponent&lt;CanvasGroup&gt;().DOFade(1, 0.8f).SetDelay(0.5f);
</code></pre>
<p><strong>Örnek2:</strong></p>
<p>Bu örnekte alpaPanelimizin canvas groupunda bulunan <strong>alpha</strong> değeri değeri 255</p>
<pre><code> public GameObject alphaPanel;
 alphaPanel.GetComponent&lt;CanvasGroup&gt;().DOFade(0, 2f);
</code></pre>
<h3 id="doscaleint-value-int-duration">DOScale(int value, int duration)</h3>
<p><strong>DOFade</strong> ile Aynı mantık ile bakacak olursak animasyonlu bir şekilde sahnede belirmesini sağlayan bir fonksiyonumuzdur. İlk değerimiz ulaşacağı son boyutu ikinci değerimiz ise bunu gerçekleştireceği zamanı verir.</p>
<p><strong>Önemli Not</strong><br>
Kodun Sonundaki  <strong>SetEase</strong> kısmı da burada anlatılmıştır.</p>
<p><strong>Örnek1:</strong></p>
<p>Panelimizin transformunda işlem yapabilmemiz için tanımlamamız gerekmektedir.</p>
<pre><code>[SerializeField]
Transform soruPaneli;
</code></pre>
<p>Soru panelimizin sahne başladığında görünmez başlamasını istiyorum.</p>
<pre><code>Void Start()
{
soruPaneli.GetComponent&lt;RectTransform&gt;().localScale = new Vector3(0, 0, 0);
     
}
</code></pre>
<p>Animasyonlu bir şekilde büyümesini sağladığımız fonksiyonumuz</p>
<pre><code> void SoruPaneliniAc()
}
 soruPaneli.GetComponent&lt;RectTransform&gt;().DOScale(1, 0.5f).SetEase(Ease.OutBack);
}
</code></pre>
<h3 id="seteaseease.parametre">SetEase(Ease.parametre)</h3>
<p>Kodumuzun sonuna yazcağımız bu ilave kod son bir animasyon ekleyerek işlerinizi çok daha profesyonel göstermektedir. Deneyerek farkı görebilirsiniz. Kodumuzda kullandığımız <strong>SetEase(Ease.OutBack)</strong> kısmı panelimizin sahnede alacağı son scale değeri 1 ise bunu 1.01 yapıp tekrar 1 e döndürerek son bir hareket kazandırmış oluyor.</p>

## Bir Butonu Pasif Hale Getirmek (Buton Gözükecek Ama Basılamayacak)

[EXTRA]Kullanıcın bastığı butonun hangisi olduğunu öğrenmek işin bu kodları yazıyoruz.

    Game Object geçerliKale;
    geçerliKare = UnityEngine.EventSystems.EventSystem.current.currentSelectedGameObject;

Asıl meselemiz olan butonu pasif hale getirme

    geçerliKare.transform.GetComponent<Button>().interactable = false;

<hr>


<blockquote>
<h2 id="game-manager"><strong>GAME MANAGER</strong></h2>
</blockquote>

## Temel Fonksiyonlar
**void Update()** : Saniyede fps değeri kadar çalışır. Örnek olarak eğer cihazınızın fps değeri 60 ise bu fonksiyon 1 saniyede 60 defa çalıştırılır.



<h2 id="oyundan-çıkış">Oyundan Çıkış</h2>
<h3 id="application.quit">Application.Quit()</h3>
<p>Uygulamadan çıkılmasını sağlar.</p>
<h2 id="sahneler-arası-geçiş">Sahneler Arası Geçiş</h2>
<h3 id="scenemanager.loadscenesahnenin-ismi">SceneManager.LoadScene(“sahnenin ismi”);</h3>
<p>Sahneler arası geçişi sağlamaktadır.<br>
Genellikle UI kısımda butonlara atanır.</p>
<p><strong>Örnek:</strong></p>
<pre><code>using UnityEngine.SceneManagment;
SceneManager.LoadScene("GameLevel");
</code></pre>
<p><strong>NOT</strong><br>
Bazen unity editörü şu hatayı verebilir ve kodun altını çizebilir:</p>
<pre><code>"Assets/MenuManager.cs(7,17): error CS0103: The name `SceneManager' does not exist in the current context."
</code></pre>
<p>Bu tip bir durumu komutumuzun uzun versiyonunu yazarak çözüme kavuştururuz.</p>
<pre><code>UnityEngine.SceneManagement.SceneManager.LoadScene("GameLevel");
</code></pre>
<h2 id="i̇şlemleri-sıralı-bir-şekilde-yapma-veya-gecikmeli-yapma">İşlemleri Sıralı Bir Şekilde Yapma veya Gecikmeli Yapma</h2>
<h3 id="coroutine-ve-ienumerator">Coroutine ve IEnumerator</h3>
<p><strong>Örnek1:</strong><br>
Game Object türünden bir küp tanımladık</p>
<pre><code>[SerializeField]
GameObject kup;
</code></pre>
<p>Sahne Başlayınca <strong>IEnumerator</strong> ön ekli fonksiyonumuzun çağrılmasını sağladık<br>
<strong>IEnumerator</strong> ön ekli fonksiyonlar <strong>Coroutine</strong> kullanılarak çağrılır</p>
<pre><code>void start
{
    StartCoroutine(GorulunurluguKapat());
    ds
  
}
</code></pre>
<p>Bu fonksiyonlarda <strong>yield</strong> anahtar kelimedir asıl görev onların üstündedir onlarsız yazamayız<br>
3 saniye bekledikten sonra alttaki işlemi yap yani küpü kapat<br>
2 saniye bekledikten sonra altındaki işlemi yap yani küpü aç</p>
<pre><code>IEnumerator GorulunurluguKapat() 
{
    yield return new WaitForSeconds(3f);,
    kup.setActive(false);
    yield return new WaitForSeconds(2f);,
    kup.setActive(true);
    
}
</code></pre>
<p><strong>NOT</strong><br>
Eğer update fonksiyonu gibi bir sonraki frame işlem yapmak istersek bu kodu kullanırız</p>
<pre><code>  yield return null;
</code></pre>
<p><strong>Örnek2</strong><br>
Bu örnekte amacım bölüm butonlarını tek tek yanıp sönen bir animasyon şeklinde sahneye dizmek.</p>
<p><strong>Dikkat</strong><br>
Hiyerarşi alanına button eklemiyorum, image ekleyip component olarak buton ekliyorum.</p>
<p>karePrefabım bir image onun ve onun hiyeyarşisi altında bulunan bir texten oluşuyor. Aynı zamanda ileride buton işlevi görmesi için butonu component olarak ekledim. Ve son olarak animasyonu yapabilmem için canvas group bulunmakta.</p>
<pre><code>[SerializeField]
GameObject karePrefab;
</code></pre>
<p>karelerPaneli butonlarımın art arda düzenli bir şekilde çıkacağı konumları belirtebilmem için oluşturduğum bir panel.</p>
<pre><code>[SerializeField]
Transform karelerPaneli;
</code></pre>
<p>Ve oluşturacağım karelerde işlem yapabilmem için boş bir dizi</p>
<pre><code>private GameObject[] karelerDizisi = new GameObject[25];
</code></pre>
<p>Sahnem başlayınca butonlarımı teker teker çıkarmaya başlaması için start fonksiyonunda kullanıyoruz</p>
<pre><code>void Start()
    {
        KareleriOLustur();
        
    }
</code></pre>
<p>Kareleri oluşturduğum ve boş diziyi doldurduğum fonksiyonum</p>
<pre><code> public void KareleriOLustur()
 {
    //25  adet eleman bastırıcam
    for(int i = 0; i &lt; 25; i++)
    {
      //kareyi panelin içinde oluşturuyorum
      //panelde grid layout group ekli
      GameObject kare = Instantiate(karePrefab,karelerPaneli);
    
   	   //diziye eleman olarak ekletiyorum
   	   karelerDizisi[i] = kare;
   
     }

    //tek tek gelmesi için gecikmeyi başlatıyorum
    StartCoroutine(DoFadeRoutine());
    
}
</code></pre>
<p>Animasyonları gerçekleştirerek ekrana yazdığım fonksiyonum</p>
<pre><code>IEnumerator DoFadeRoutine()
{
    //25 kere yapıcam cünkü 25 elemanım var
    for(int i = 0; i &lt; 25; i++)
    {
        //canvas grouplatın ulaşıp saydamlıklarını arttırıyrum ve bunu 0.2 saniyede yapıyorum
        karelerDizisi[i].GetComponent&lt;CanvasGroup&gt;().DOFade(1, 0.2f);

        //yeni kareyi basmadan önce 0.2 saniye bekletiyorm
        yield return new WaitForSeconds(0.2f);

    }
}
</code></pre>
<h2 id="süre-saydırma---bekletme">Süre Saydırma - Bekletme</h2>
<h3 id="waitforsecondsfloat-beklenilecek_süre">WaitForSeconds(float beklenilecek_süre)</h3>
<p>Fonksiyon aldığı değer kadar süre sayar</p>
<p><strong>Örnek1:</strong><br>
WaitForSeconds(3f);</p>
<h2 id="random--sayı-üretme">Random  Sayı Üretme</h2>
<h3 id="random.rangeint-dahil-int-dahil-değil">Random.Range(int dahil, int dahil değil)</h3>
<p><strong>Örnek1:</strong><br>
int x = Random.Range(1,13);</p>
<p>1&lt;= x &lt; 13</p>
<h2 id="bir-nesnenin-çocuk-nesnesine-ulaşmak">Bir Nesnenin Çocuk Nesnesine Ulaşmak</h2>
<h3 id="transform.getchildint-index"># Transform.GetChild(int index)</h3>
<p><strong>Not:</strong><br>
Getchild(0) ile ilk elemana erişirsin.<br>
int index = 0 =&gt; ilk eleman<br>
int index = 1 =&gt; ikinci eleman</p>
<p><strong>Örnek 1:</strong></p>
<pre><code> public void Example()

    {
//Assigns the transform of the first child of the Game Object this script is attached to.
meeple = this.gameObject.transform.GetChild(0);  
  
//Assigns the first child of the first child of the Game Object this script is attached to.
grandChild = this.gameObject.transform.GetChild(0).GetChild(0).gameObject;
}
</code></pre>

## Butona OnClick Özelliğini Dinamik Olarak Atamak

**kare** nesnemize basıldığında **butonaBasildi** adlı fonksiyonumuzun çalışmasını istiyoruz.

    kare.transform.GetComponent<Button>().onClick.AddListener(() => butonaBasildi());


## Kullanıcın seçtiği Game Objeyi Öğrenme

Kullanıcın o an etkilişime girdiği, üstüne bastığı game objeyi öğrenmek

	    Game Object OgrenmekIstedgimizGO;
        OgrenmekIstedgimizGO = UnityEngine.EventSystems.EventSystem.current.currentSelectedGameObject;

<blockquote>
<h2 id="game-manager"><strong>C# FUNDEMENTAL</strong></h2>
</blockquote>

## String Bir Değeri İnteger Türüne Dönüştürmek
b stringini integera çevirerek a değişkenine atamasını yaptık
 

    int a;
    string b = "2";
    
    a = int.Parse(b);

## Başka Bir Scripten Fonksiyon Çağırmak

Ulaşmak istediğim script = a,
Bulunduğum scripte a yı çağıracağım değişkenimin ismi = b olsun


    a b;
    b = Object.FindObjectOfType<a>();
    b.CAGIRMAK ISTEDIGIM FONKSIYONUMUN ADI;






<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzAxNDgxMDgsNjU0ODY3ODk0LDE5MT
I4ODk0OTksLTQ4NjY2MTk0MCwtMzI0ODc2MjAzLC0xNjQ2OTM1
NDM0LDE5NDg4NTUxMDIsLTcxOTA0NDMzNiwtMTY0OTY4MDI1NC
wyMDg3NTkxOTc0LC0yNTk4MTMzN119
-->