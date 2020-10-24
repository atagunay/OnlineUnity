---


---

<h1 id="uni̇ty-dökümantasyonu">UNİTY DÖKÜMANTASYONU</h1>
<blockquote>
<h2 id="user-interface"><strong>USER INTERFACE</strong></h2>
</blockquote>
<h2 id="dofadefloat-bitiş_değeri-float-zamanlama">DOFade(float bitiş_değeri, float zamanlama)</h2>
<p>Bu fonksiyonun temel amacı objelerin renklerindeki <strong>“A”</strong> değerini yani saydamlığını belirli bir süre zarfında değiştirmektir. En çok kullandığım objeler buton ve panellerdir.</p>
<p>Ben bu fonksiyonu oyunumun başlangıç menüsü açılırken butonların animasyonlu bir şekilde gelmesi için kullandım.</p>
<h4 id="kullanimi">KULLANIMI</h4>
<p>Assetstoredan <strong>DOTween (HOTween v2) Free</strong> eklentisini indirip projemize ekliyoruz.</p>
<p>Kullanacağımız classımıza <strong>using DG.Tweening</strong> şeklinde ekliyoruz.</p>
<p>Saydamlaştırmayı istediğimiz objemize(benim için buton) canvas group eklememiz gerekmektedir.</p>
<p>Kodlara geçmeden öncede butonlarımızın renk ayarlarından <strong>A</strong> değerini sıfır yapıyoruz.</p>
<p><strong>Örnek1:</strong></p>
<pre><code>[SerializeField]
 GameObject startBtn, exitBtn;
</code></pre>
<p>Butonlarımızın <strong>A</strong> değeri sıfırdı fonksiyonumuzun ilk parametresi 		A’nın bitiş değerini ikinci parametresi ise bu işlemi yapacağı süreyi söylemektedir</p>
<pre><code>startBtn.GetComponent&lt;CanvasGroup&gt;().DOFade(1, 0.8f);

exitBtn.GetComponent&lt;CanvasGroup&gt;().DOFade(1, 0.8f).SetDelay(0.5f);
</code></pre>
<p><strong>Örnek2:</strong></p>
<p>Bu örnekte alpaPanelimizin <strong>A</strong> değeri 255</p>
<pre><code> public GameObject alphaPanel;
 alphaPanel.GetComponent&lt;CanvasGroup&gt;().DOFade(0, 2f);
</code></pre>
<hr>
<blockquote>
<h2 id="game-manager"><strong>GAME MANAGER</strong></h2>
</blockquote>
<h2 id="application.quit">Application.Quit()</h2>
<p>Uygulamadan çıkılmasını sağlar.</p>
<h2 id="scenemanager.loadscenesahnenin-ismi">SceneManager.LoadScene(“sahnenin ismi”);</h2>
<p>Sahneler arası geçişi sağlamaktadır.<br>
Genellikle UI kısımda butonlara atanır.</p>
<p><strong>Örnek:</strong></p>
<pre><code>SceneManager.LoadScene("GameLevel");
</code></pre>

