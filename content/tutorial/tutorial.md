---
id: tutorial
title: "Öğretici: React'a giriş"
layout: tutorial
sectionid: tutorial
permalink: tutorial/tutorial.html
redirect_from:
  - "docs/tutorial.html"
  - "docs/why-react.html"
  - "docs/tutorial-ja-JP.html"
  - "docs/tutorial-ko-KR.html"
  - "docs/tutorial-zh-CN.html"
  - "docs/tutorial-tr.html"
---

Bu öğretici, herhangi bir React bilginizin olmadığını varsayar.

## Öğreticiye Başlamadan Önce {#before-we-start-the-tutorial}

Bu öğreticide küçük bir oyun geliştireceğiz. **Oyun yapmadığınızdan dolayı bu öğreticiyi atlamak istiyor olabilirsiniz -- ama bir şans vermeniz iyi olacaktır.** Zira bu öğreticide edineceğiniz teknikler herhangi bir React uygulaması geliştirmek için temel niteliğindedir, ve bu temeller üzerinde uzmanlaşmak React'ı daha derinlemesine öğrenmenizi sağlayacaktır.

>İpucu
>
>Bu öğretici, **kodlayarak öğrenmek** isteyen kişiler için tasarlanmıştır. Eğer bu konseptleri her yönüyle edinmek isterseniz [adım adım öğrenme rehberini](/docs/hello-world.html) inceleyebilirsiniz. Bu öğretici ve adım adım öğrenme rehberinin birbirini tamamlayıcı nitelikte olduğunu görebilirsiniz.  

Bu öğretici birkaç bölüme ayrılmıştır:

* [Öğretici İçin Kurulum](#oretici-icin-kurulum) bu öğreticiyi takip etmek için size bir **başlangıç noktası** sunar. 
* [Genel bakış](#overview) React'ın **temellerini** öğretecektir: `component`'lar, `prop`'lar, ve uygulama `state`'i.
* [Oyunun Tamamlanması](#completing-the-game) React geliştirimindeki **en yaygın teknikleri** aktaracaktır.
* [Zaman Yolculuğunun Eklenmesi](#zaman-yolculugunun-eklenmesi) React'ın benzersiz özelliklerini ile ilgili **daha derinlemesine** kavramanızı sağlayacaktır.

Bu öğreticiden yararlanmanız için tüm bölümleri tamamen bitirmek zorunda değilsiniz. Bir-iki bölüm tamamlasanız bile sizin için yararlı olacaktır.

Bu öğreticiyi takip ederken kodları kopyala-yapıştır yaparak denemenizde hiçbir sorun yoktur fakat elle kodlayarak ilerlemenizi tavsiye ederiz. Bu sayede kas hafızanız gelişecek ve React'ı daha güçlü bir şekilde öğrenmiş hale geleceksiniz. 

### Ne kodlayacağız? {#what-are-we-building}

Bu öğreticide, React ile bir tic-tac-toe (XOX oyunu) nasıl geliştirilir onu göstereceğiz. 

**[Buradan](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)** oyunun son halini görebilirsiniz. Eğer kodlar size karışık geliyorsa veya koda aşina değilseniz endişelenmeyin. Çünkü bu öğreticinin amacı, React'ın ve React'taki kod yapısının anlaşılmasında size yardımcı olmaktır. 

Bu öğreticiye başlamadan önce yukarıda belirttiğimiz tic-tac-toe oyununu incelemenizi tavsiye ediyoruz. Oyunu oynadığınızda farkedeceğiniz gibi oyun tahtasının sağında numaralandırılmış bir liste bulunmaktadır. Bu liste size, oyunda oluşan hamlelerin bir geçmişini sunar ve oyunda ilerledikçe liste de otomatik olarak güncellenir.

tic-tac-toe oyununu inceledikten sonra kapatabilirsiniz. Bu öğreticide daha basit bir şablondan başlayacağız. Sonraki adımımızda oyunu geliştirmek için gereken ortamın kurulumuna değineceğiz.

### Ön gereksinimler {#prerequisites}

Bu öğreticide, HTML ve JavaScript'i az-çok bildiğinizi varsayacağız, fakat herhangi bir programlama dilinden gelmiş olsanız bile aşamaları takip edebiliyor olmalısınız. Ayrıca temel programlama konseptleri olan fonksiyonlar, nesneler, diziler ve daha az oranda da sınıflar hakkında aşina olduğunuzu varsayıyoruz.

Eğer JavaScript hakkında bilgi edinmeniz gerekiyorsa, [bu rehberi](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) okumanızı tavsiye ederiz. JavaScript'in en güncel versiyonu olan ES6'dan bazı özellikleri kullanıyoruz. Bu öğreticide de ES6 özelliği olan [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [`class`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), ve [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) ifadelerini kullanıyor olacağız. [Babel REPL](babel://es5-syntax-example)'ı kullanarak ES6 kodunun derlenmiş halini görebilirsiniz.

## Öğretici İçin Kurulum {#setup-for-the-tutorial}

Bu öğreticiyi tamamlamanın iki yolu bulunmaktadır: kodu tarayıcınızda yazabilir veya bilgisayarınızdaki yerel geliştirim ortamını kurabilirsiniz. 

### Kurulum Seçeneği 1: Kodu Tarayıcıda Yazma {#setup-option-1-write-code-in-the-browser}

Başlamanız için en kolay yol budur!

Öncelikle, bu **[başlangıç kodunu](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** yeni sekmede açınız. Yeni sekme boş bir tic-tac-toe oyunu ve React kodu görüntülüyor olacaktır. Bu öğreticide React kodunu düzenliyor olacağız.

Bu seçeneği istiyorsanıaz ikinci seçeneği es geçebilir, ve [Genel bakış](#overview) bölümüne giderekn genel bilgi edinebilirsiniz.

### Kurulum Seçeneği 2: Yerel Geliştirim Ortamı {#setup-option-2-local-development-environment}

Bu seçenek tamamen isteğe bağlıdır ve bu öğretici için gerekli değildir!

<br>

<details>

<summary><b>İsteğe bağlı: Tercih ettiğiniz metin editörünü kullanarak projeyi yerel ortamınızda geliştirmeniz için yönergeler</b></summary>

Bu kurulum daha fazla çalışmayı gerektirir fakat aynı zamanda favori editörünüzü kullanarak projeyi tamamlamanıza da olanak tanır. İzlenecek adımlar aşağıdaki gibidir:

1. [Node.js](https://nodejs.org/en/)'in güncel versiyonunun yüklü olduğundan emin olunuz.
2. Yeni bir proje oluşturmak için [Create React App uygulaması kurulum yönergelerini](/docs/create-a-new-react-app.html#create-react-app) takip ediniz.

```bash
npx create-react-app my-app
```

3. Yeni projenin `src/` dizininin içerisindeki tüm dosyaları siliniz

> Not:
>
>**`src` dizininin kendisini silmeyiniz, sadece içerisinde yer alan ve varsayılan olarak gelen kaynak dosyalarını siliniz.** Sonraki adımda oluşan varsayılan dosyaları, bu projenin dosyaları ile değiştireceğiz. 

```bash
# Proje dizinindeki src'nin içine gitmek için aşağıdaki komutlar kullanılır:
cd my-app
cd src

# Daha sonra dizin içerisindeki dosyaları silmek içim işletim sistemine göre rm veya del komutu kullanılır.
# Eğer Mac veya Linux kullanıyorsanız:
rm -f *

# Windows kullanıyorsanız:
del *

# Then, switch back to the project folder
cd ..
```

4. `src/` dizininde `index.css` dosyasını oluşturup [buradaki CSS kodunu](https://codepen.io/gaearon/pen/oWWQNa?editors=0100) ekleyiniz.

5. `src/` dizininde `index.js` dosyasını oluşturup [buradaki JS kodunu](https://codepen.io/gaearon/pen/oWWQNa?editors=0010) ekleyiniz.

6. `src/` dizinindeki `index.js` dosyasını açıp en üste bu 3 satırı ekleyiniz:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

Artık projeyi çalıştırabilirsiniz. Proje dizininde iken `npm start` yazıp enter'a bastığınızda, tarayıcıda `http://localhost:3000` url'i açılacak ve devamında boş bir tic-tac-toe oyunu görüyor olacaksınız.

Metin editörünüzde, kodun renkli halde görüntülenmesini sağlamak için [buradaki yönergeleri](https://babeljs.io/docs/editors/) izlemenizi tavsiye ederiz.

</details>

### Bir Yerde Takıldım, Yardım! {#help-im-stuck}

Eğer bu öğreticiyi takip ederken herhangi bir yerde takıldıysanız, [topluluk destek kaynaklarına](/community/support.html) bakınız. Özellikle Discord'da yer alan [Reactiflux Chat](https://discord.gg/0ZcbPKXt5bZjGY5n) kanalı, hızlıca yardım almak için oldukça elverişlidir. Eğer bir cevap alamadıysanız veya hala takıldığınızdan dolayı devam edemiyorsanız lütfen bize GitHub üzerinden issue açınız devamında size yardımıcı olacağız.

## Genel Bakış {#overview}

Kurulumu tamamladığınıza göre haydi şimdi React'e giriş yapalım!

### React Nedir? {#what-is-react}

React, kullanıcı arayüzleri oluşturmak için açık, verimli ve esnek bir JavaScript kütüphanesidir. Component (bileşen) denilen küçük ve izole parçalar sayesinde karmaşık arayüz birimlerini oluşturmanıza olanak tanır. 

React'te birkaç tipte component bulunmaktadır. `React.Component` alt sınıflarına değinelim:

```javascript
class AlisverisListesi extends React.Component {
  render() {
    return (
      <div className="alisveris-listesi">
        <h1>{this.props.adi}e ait Alışveriş Listesi</h1>
        <ul>
          <li>Elma</li>
          <li>Armut</li>
          <li>Muz</li>
        </ul>
      </div>
    );
  }
}

// Örnek kullanım: <AlisverisListesi adi="Mehmet" />
```

Birazdan üstte kullandığımız XML-tarzı etiketlere değineceğiz. Component'leri kulanarak ekranda görmek istediğimiz arayüz birimlerini React'a belirtmiş oluyoruz. Verilerimiz değiştiği zaman React, etkili bir şekilde component'lerimizi güncelleyecek ve tekrar render edecektir (arayüze işleyecektir). 

Burada AlisverisListesi için bir **React component sınıfıdır**, veya **React component tipidir** diyebiliriz. Bir component, "properties" (özellikler)'in kısaltması olan `props` adı verilen parametreleri alır, ve `render` metodu aracılığıyla görüntülemek için bir görünüm hiyerarşisi (XML) return eder. 

`render` metodu, ekranda neyi görüntülemek istiyorsanız onunla ilgili bir *tanımlama* return eder. React bu tanımlamayı alır ve görüntüler. Bilhassa `render` metodu, neyi render edeceği ile ilgili bir tanımlama olan **React elemanı** return eder. Birçok React geliştiricisi, bu tanımlamaları kolayca kodlamayı sağlayan ve "JSX" denilen özel bir kod dili kullanır. JSX olan `<div />` içeriği ise derleme zamanında `React.createElement('div')` JavaScript metod çağrısına dönüştürülür. Üstteki örneğin derlenmiş hali aşağıdaki gibidir:

```javascript
return React.createElement('div', {className: 'alisveris-listesi'},
  React.createElement('h1', /* ... h1 içeriği ... */),
  React.createElement('ul', /* ... ul içeriği ... */)
);
```

[Tam hali için tıklayınız.](babel://tutorial-expanded-version)

Eğer `createElement()` fonksiyonunu merak ediyorsanız, [API dokümanında](/docs/react-api.html#createelement) daha detaylı şekilde ele alınacaktır, fakat bu öğreticide `createElement()` fonksiyonunu kullanmayacağız. Bunun yerine JSX notasyonunu ele alacağız.

JSX, JavaScript'in bütün gücünü kullanacak şekilde tasarlanmıştır. Bu sayede JSX kodu içerisinde süslü parantezler kullanarak herhangi bir JavaScript ifadesini çalıştırabilirsiniz. Her React elemanı, bir değişkende saklayabileceğiniz veya uygulama içerisinde herhangi bir yere aktarabileceğiniz bir JavaScript nesnesidir.

Yukarıdaki `AlisverisListesi` component'i, yalnızca `<div />` ve `<li />` gibi yerleşik DOM bileşenlerini render eder. Fakat uygulamanıza özel React component'leri oluşturarak ve birleştirerek bu React component'lerinin de render edilmesini sağlayabilirsiniz. Örneğin sadece `<AlisverisListesi />` yazarak bütün alışveriş listesinin görüntülenmesini sağlayabiliriz. Her React component'i izole edilmiştir ve birbirlerinden bağımsız olarak çalışabilir. Bu sayede basit component'leri bir araya getirerek kompleks kullanıcı arayüzleri oluşturabilirsiniz.

## Başlangıç Kodunun İncelenmesi {#inspecting-the-starter-code}

Eğer bu öğreticiyi **tarayıcınızda** takip edecekseniz, **[başlangıç kodunu](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** yeni sekmede açınız. Eğer öğreticiyi **yerel makinenizde** takip edecekseniz, bunun yerine proje dizininde yer alan `src/index.js` dosyasını açınız (bu dosyaya daha önce [kurulum](#setup-option-2-local-development-environment) aşamasında değinmiştik). 

Bu başlangıç kodu, yapacağımız proje ile ilgili bir temel niteliğindedir. Size CSS kodlarını hazır olarak sunduk, bu sayede CSS ile uğraşmaksızın yalnızca React'i öğrenmeye ve tic-tac-toe oyununun programlanmasına yoğunlaşacabileceksiniz.

Kodu incelediğinizde aşağıdaki 3 React component'ini fark edeceksiniz:

* Square (Kare)
* Board (Tahta)
* Game (Oyun)

Şu an Square component'i yalnızca bir adet `<button>` elemanını, Board ise 9 adet Square component'ini render ediyor. Game component'i ise Board component'ini ve daha sonra değiştireceğimiz bir kısa metni render ediyor. Henüz uygulama içerisinde etkileşimli bir component yer almamaktadır.

### Prop'lar Aracılığıyla Veri Aktarımı {#passing-data-through-props}

Şimdi işe koyulalım ve Board component'inden Square component'imize bazı verileri göndermeyi deneyelim.

Board'ın `renderSquare` metodunda, `value` (değer) adındaki prop'u Square'e gönderecek şekilde kodu değiştirelim:

```js{3}
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Square's `render` metodunu ilgili değeri göstermesi için `{/* TODO */}` kısmını `{this.props.value}` şekilde değiştirelim:

```js{5}
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

Öncesi:

![React Devtools](../images/tutorial/tictac-empty.png)

Sonrası: Eğer değişiklikleri doğru bir şekilde uyguladıysanız render işlemi bitiminde her karede içerisinde bir sayı görüyor olmalısınız. 

![React Devtools](../images/tutorial/tictac-numbers.png)

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)**

Tebrikler! Board component'inden Square component'ine "prop ile veri geçirmeyi" başardınız. React uygulamalarında prop'ların ebeveyn component'ten çocuk component'e geçişi sayesinde veri akışının oluşması sağlanır.

### Etkileşimli bir Component Yapımı {#etkilesimli-bir-component-yapimi}

Haydi şimdi Square component'ine tıkladığımızda içini "X" ile dolduralım. 
Öncelikle, Square component'inin `render()` fonksiyonundan dönen button etiketini bu şekilde değiştirelim:

```javascript{4}
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() { alert('click'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

Şimdi herhangi bir kareye tıkladığımızda tarayıcıda bir alert mesajı görüntülenecektir. 

>Not:
>
>Daha az kod yazmak ve [`this`'in kafa karıştırıcı kullanımından](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/) kaçınmak için, event handler gibi kısımlarda [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)'ını kullanacağız:
>
>```javascript{4}
>class Square extends React.Component {
>  render() {
>    return (
>      <button className="square" onClick={() => alert('click')}>
>        {this.props.value}
>      </button>
>    );
>  }
>}
>```
>
>Farkedeceğiniz üzere, `onClick={() => alert('click')}` kısmında butonun `onClick` prop'una *bir fonksiyon* ataması gerçekleştiriyoruz. Bu fonksiyon sadece butona tıkladığımızda çalışıyor. Genellikle bir yazılımcı hatası olarak parantezli ok `() =>` ifadesinin unutulması yerine direkt olarak `onClick={alert('click')}` ifadesinin yazılması gerçekleşebiliyor. Bu durumda tıklama anında gerçekleşmesi istenen olay yanlış bir şekilde çalışarak, component tekrar render edildiğinde gerçekleşmiş oluyor.

Sonraki adım olarak, Square component'inin tıklandığı zamanı "hatırlamasını" ve "X" işareti ile doldurulmasını isteyeceğiz. Bir şeyleri "hatırlamak" için component'ler **state**'i (durum) kullanırlar.

React component'leri constructor (yapıcı) fonksiyonlarında `this.state`'e atama yaparak bir state'e sahip olurlar. React component'i içerisinde tanımlanan `this.state` özelliğinin erişim belirleyicisi private olarak düşünülmelidir. Şimdi Square'in mevcut değerini `this.state` içerisinde saklayalım ve Square'e tıklandığında değiştirelim. 

Öncelikle class'a bir constructor ekleyeceğiz ve içerisinde state'in başlangıç değerlerini oluşturacağız:

```javascript{2-7}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

>Not:
>
>[JavaScript class'larında](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), alt sınıfın constructor'ını oluştururken her zaman `super` fonksiyonunu çağırmanız gerekmektedir. Her bir React component class'ı içerisinde `super(props)` çağrısı ile başlayan bir constructor barındırmalıdır.

Şimdi Square'e tıklandığında state'in mevcut değerinin görüntülenmesi için Square'in `render` metodunu değiştireceğiz:

* `<button>` etiketi içerisinde yer alan `this.props.value` yerine `this.state.value` yazalım.
* `() => alert()` event handler'ını `() => this.setState({value: 'X'})` ile değiştirelim.
* Okunabilirliği arttırmak için `className` ve `onClick` prop'larını ayrı satırlara alalım.

Bu değişikliklerden sonra Square'in `render` metodundan dönen `<button>` etiketi aşağıdaki gibi görüntülenecektir:

```javascript{12-13,15}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

Square'in `render` metodundaki bir `onClick` metodundan `this.setState`'in çağrılması ile, Square'in `<button>` elemanına her tıklandığında tekrar render edilmesi gerektiğini React'a belirtiyoruz.  Güncelleme sonrasında Square'in `this.state.value` değerine `'X'` ataması gerçekleşiyor, ve bu sayede oyun tahtasında 'X''i görüyoruz. Herhangi bir kareye tıklandığı anda içerisinde 'X' görüntülenecektir.

Bir component'teki `setState` fonksiyonunu çağırdığınızda, React otomatik olarak içerisindeki çocuk component'leri de güncellemiş oluyor.

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)**

### Geliştirici Araçları {#developer-tools}

[Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) ve [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) için React Devtools eklentisi sayesinde herhangi bir React component ağacını, tarayıcınızın geliştirici araçları kısmından görüntüleyebilirsiniz.

<img src="../images/tutorial/devtools.png" alt="React Devtools" style="max-width: 100%">

React DevTools, React component'lerinizin state'ini ve prop'larını kontrol etmenize olanak tanır.

React DevTools kurulumundan sonra, sayfa içerisindeki herhangi bir elemana sağ tıklayarak çıkan menüde "İncele"'yi seçerek geliştirici araçlarını açabilir, ve devamında en sağda yer alan React sekmesinde incelemelerinizi yürütebilirsiniz.

**Eklentinin CodePen ile çalışabilmesi için harici olarak birkaç adım daha vardır:**

1. CodePen'e e-posta adresiniz ile giriş yapın veya kaydolunuz (spam'lerin engellenmesi için gereklidir).
2. "Fork" butonuna basınız.
3. "Change View"'a tıklayarak devamında "Debug mode"'u seçiniz.
4. Açılan yeni sekmede, artık Devtools içerisinde React sekmesi yer alacaktır.

## Oyunun Tamamlanması {#completing-the-game}

Artık tic-tac-toe oyunumuz için temel kod bloklarına sahibiz. Oyunun tamamlanması için tahta üzerinde "X" ve "O"'ların birbiri ardına yerleştirilmesi ve devamında bir kazananın belirlenmesi için değişiklikler yapmamız gerekiyor. 

### State'in Ebeveyn Component'e Taşınması {#lifting-state-up}

Şu an her bir Square component'i oyunun state'ini değiştirebiliyor. Kazananı belirleyebilmemiz için her bir 9 square'in değerine ihtiyacımız var.

Board'ın her bir Square'e, kendi state'inin ne olduğunu sorması gerektiğini düşünebiliriz. Bu yöntem her ne kadar React'te uygulanabilir olsa da yapmanızı tavsiye etmiyoruz. Çünkü bu şekilde kod anlaşılabilirlikten uzak hale gelecek, hataların oluşmasına daha müsait olacak ve kodu refactor etmek istediğimizde bize çok daha büyük zorluklar çıkaracaktır. Bu nedenle, her bir Square'de kendi state'inin tutulmasının yerine, ebeveyn olan Board component'inde oyunun tüm state'ini tutmak en iyi yaklaşımdır. Bunun sonucunda Board component'i, her bir Square'e neyi göstermesi gerektiğini prop'lar aracılığıyla aktarır [daha önce her bir Square'e bir sayı atadığımız gibi](#passing-data-through-props).

**Birçok çocuk component'ten verilerin toplanması için veya iki çocuğun birbirleri arasında iletişim kurabilmesi için ebeveyn component'te paylaşımlı bir state oluşturmanız gerekmektedir. Ebeveyn component, prop'lar aracılığıyla state'ini çocuklara aktarabilir. Bu sayede çocuk component'ler hem birbirleri arasında hem de ebeveyn ile senkronize hale gelirler.**

State'in ebeveyn'e taşınması React component'leri refactor edilirken çok yaygın bir durumdur -- haydi şimdi bu fırsatı değerlendirelim ve işe koyulalım. Board'a bir constructor ekleyelim ve Board'ın başlangıç state'ine bir array atayarak içerisinde 9 adet null değerinin bulunmasını sağlayalım. 9 adet null, 9 kareye karşılık gelecektir:

```javascript{2-7}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  renderSquare(i) {
    return <Square value={i} />;
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

Daha sonra Board'ı doldurdukça , array içeriği aşağıdaki gibi görünmeye başlayacaktır: 

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

Board'ın `renderSquare` metodu aşağıdaki gibi görünüyor:

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Projeye başladığımızda her bir karede 0'dan 8'e kadar olan sayıları göstermek için Board'daki `value` prop'unu çocuk component'lere [aktarmıştık](#passing-data-through-props). Bir diğer önceki aşamada ise sayıların yerine [mevcut Square component'inin kendi state'i tarafından belirlenen](#making-an-interactive-component) "X" işaretinin almasını sağlamıştık. İşte bu nedenle Square component'i, Board tarafından kendisine gönderilen `value` prop'unu göz ardı ediyor.

Şimdi prop aktarma mekanizmasını tekrar kullanacağız. Bunun için her bir Square'e kendi mevcut değerini (`'X'`, `'O'`, or `null`) atamak için Board component'inde değişiklik yapalım. Board'un constructor'ında halihazırda tanımladığımız bir `squares` array'i bulunuyor. Board'un `renderSquare` metodunu, bu array'den verileri alacak şekilde değiştirelim: 

```javascript{2}
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)**

Artık her bir Square component'i `value` prop'unu alacak ve 'X', 'O' veya boş square'ler için `null` değerini edinecektir. 

Şimdi Square'e tıklandığında ne olacağona karar vermemiz gerekiyor. Board component'i artık hangi square'in doldurulacağına karar verebildiğine göre Square'e tıklandığında Board component'inin state'inin güncellenmesini sağlamalıyız. State her bir component'e private olduğundan dolayı Square üzerinden direkt olarak Board'un state'ini değiştiremeyiz. 

Board'un state'inin gizliliğini korumak için, Board'dan Square'e bir fonksiyon aktarmamız gerekiyor. Square'e her tıklama anında bu fonksiyonun otomatik olarak çağrısı gerçekleşecektir. Şimdi Board'un `renderSquare` metodunu aşağıdaki şekilde değiştirelim:

```javascript{5}
  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }
```

>Not
>
>Kodun okunabilirliği için geri dönüş elemanını birçok satıra böldük ve parantezler ekledik. Bu sayede JavaScript, `return`'den sonra otomatik olarak bir noktalı virgül eklemeyecek ve bundan dolayı kodun bozulması engellenmiş hale gelecektir.

Artık Board'dan Square'e, `value` ve `onClick` olmak üzere iki tane prop gönderiyoruz. Square'e tıklandığında ise prop olarak gelen `onClick` fonksiyonu çağrılmasına ihtiyacımız var. Bunun için Square'e aşağıdaki değişiklikleri uygulamamız gerekiyor:

* Square'in `render` metodu içerisinde yer alan `this.state.value` yerine `this.props.value` yazınız.
* Yine Square'in `render` metodundaki `this.setState()` yerine `this.props.onClick()` yazınız.
* Square artık oyunun state'ini değiştirmeyeceği için, Square'in `constructor` metodunu siliniz.

After these changes, the Square component looks like this:

```javascript{1,2,6,8}
class Square extends React.Component {
  render() {
    return (
      <button
        className="square"
        onClick={() => this.props.onClick()}
      >
        {this.props.value}
      </button>
    );
  }
}
```

Artık Square'e tıklandığında, Board tarafından aktarılan `onClick` fonksiyonu çağrılacaktır. Here's a review of how this is achieved:

1. HTML'de varsayılan olan `<button>` component'inin `onClick` prop'u React'e, tıklama olayını oluşturmasını söyler.
2. Butona tıklandığında React, Square'in `render()` metodunda tanımlanan `onClick` fonksiyonunu çalıştırır.
3. Bu fonksiyon ise, `this.props.onClick()` çağrısını gerçekleştirir. Square'in `onClick` prop'u, Board tarafından kendisine aktarılmıştır.
4. Board, Square'e `onClick={() => this.handleClick(i)}` kodunu aktardığı için, Square'e tıklandığında Board'un `this.handleClick(i)` metodu çağrılır.
5. Şu an `handleClick()` metodunu tanımlamadığımız için kodumuz hata verecektir.

>Not
>
>DOM'daki `<button>` elemanı varsayılan component olarak geldiği için, `onClick` fonksiyonu, React için özel bir anlam ihtiva eder. Fakat Square gibi custom component'lerde, prop isimlendirmesi size kalmıştır. Bu nedenle Square'in `onClick` prop'unu veya Board'un `handleClick` metodunu daha farklı şekilde isimlendirebilirsiniz. Ancak React'teki isimlendirme kuralına uymak gereklidir. Bu kural şu şekildedir: olayları temsil eden prop'lar için `on[Olay]`, olayları handle eden metodlar için ise `handle[Olay]` ifadeleri kullanılır. 

Square'e tıkladığımızda, `handleClick`'i tanımlamadığımız için hata aldığımızdan bahsetmiştik. Gelin şimdi Board sınıfına `handleClick`'i ekleyelim:

```javascript{9-13}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)**

Bu değişikliklerden sonra, oyundaki karelere tıkladığımızda içeriğinin "X" ile doluyor olduğunu tekrar görebiliyoruz. Fakat, artık state'in her bir Square'de ayrı ayrı yer alması yerine Board component'inde barındırılmış hale geldi. Bu sayede Board'daki state değiştiğinde tüm Square component'leri otomatik olarak tekrar render edilecektir. Bunun yanında, bütün Square'lerin state'inin Board component'inde tutulması, gelecekte kazananı belirlememiz için önemli bir yol teşkil edecektir.

Square component'leri artık state'i direkt olarak değiştirmediği için, değerleri Board component'inden alıyorlar ve tıklandıklarında Board'u haberdar ediyorlar. React terminolojisinde Square component'leri için **controlled components** (kontrollü bileşenler) adı verilir. Çünkü tüm kontrol Board component'inin elindedir. 

Fark ettiyseniz `handleClick` fonksiyonu içerisinde, halihazırda var olan `squares` array'ini direkt olarak değiştirmek yerine, `.slice()`'ı kullanarak bir kopyasını oluşturduk ve bu kopyayı değiştirdik. Sonraki bölümde neden `squares` array'inin bir kopyasını oluşturduğumuza değineceğiz. 

### Neden Immutability Önemlidir {#why-immutability-is-important}

**Immutability**, anlam olarak **mutate** (değişmek) kelimesinin zıttı olan **değişmezlik** kavramını oluşturmaktadır. Önceki kod örneğinde, mevcut `squares` array'ini değiştirmek yerine array'in `.slice()` metodu ile bir kopyasının oluşturulması gerektiğini önermiştik. Şimdi ise immutability'i ve immutability'i öğrenmenin neden önemli olduğunu tartışacağız.

Genellikle verinin değiştirilmesi için iki farklı yaklaşım vardır. İlk yaklaşımda, verinin değerleri direkt olarak değiştirilerek ilgili verinin değişmesi (mutate) sağlanır. İkinci yaklaşımda ise, ilgili veri kopyalanarak, kopya veri üzerinde istenen değişiklikler gerçekleştirildikten sonra kopya verinin, ana veriye atanması işlemidir.

#### Mutasyon Kullanılarak Verinin Değiştirilmesi {#data-change-with-mutation}
```javascript
var oyuncu = {skor: 1, adi: 'Zafer'};
oyuncu.skor = 2;
// Oyuncu nesnesinin son hali: {score: 2, name: 'Jeff'}
```

#### Mutasyon Kullanılmadan Verinin Değiştirilmesi {#data-change-without-mutation}
```javascript
var oyuncu = {skor: 1, adi: 'Zafer'};

var yeniOyuncu = Object.assign({}, oyuncu, {skor: 2});
// Şu an oyuncu nesnesi değişmedi, fakat oyuncu nesnesinden yeniOyuncu nesnesi oluşturuldu: {skor: 2, adi: 'Zafer'}

// Object spread syntax proposal'ı kullanarak aşağıdaki gibi de yazabilirsiniz:
// var yeniOyuncu = {...oyuncu, skor: 2};
```

Sonuç iki durumda da aynı oldu ama direkt olarak veriyi değiştirmeden kopya üzerinde değişiklikler yapmanın aşağıdaki gibi birçok yararı vardır. 

#### Karmaşık Özellikleri Basit Hale Getirir {#complex-features-become-simple}

Immutability sayesinde karmaşık özellikleri kodlamak çok daha kolaydır. Bu öğreticinin sonunda, tic-tac-toe oyunundaki hamlelerin geçmişini incelemeyi ve önceki hamlelere geri dönmeyi sağlayan "zaman yolculuğu" özelliğini kodlayacağız.  Bu özellik sadece oyunlarda değil birçok uygulamada ileri ve geri alma işlemlerinin kurgulanması için bir gereksinim teşkil edebilir. Direkt olarak veri mutasyonundan kaçınarak, oyunun önceki versiyonlarını oyun geçmişinde bozmadan tutabilir ve daha sonra, önceki bir versiyona geri dönmeyi sağlayabilirsiniz.

#### Değişikliklerin Tespit Edilmesini Kolaylaştırır {#detecting-changes}

Mutable nesneler, direkt olarak değiştirilebildikleri için, değişip/değişmediklerinin tespit edilmesi güçtür. Değişikliğin tespit edilebilmesi için, nesnenin öneki kopyaları ile kendisinin karşılaştırılması ve bütün nesne ağacı üzerinde gezilmesi gereklidir.

Immutable nesnelerdeki değişikliklerin tespit edilmesi daha kolaydır. Immutable nesne, öncekinden farklı bir değişkene referans edilmişse o halde nesne değişmiştir diyebiliriz.

#### Tekrar Render Etme Zamanı Kolayca Belirlenebilir {#determining-when-to-re-render-in-react}

React'te Immutability'nin ana faydası ise, _pure component_'ler (saf/katıksız bileşenler) yapmayı kolaylaştırmasıdır. Immutable veriler, değişiklik yapıldığını kolayca tespit edebilirler. Bu sayede değişiklik olduğunda ilgili component'in tekrar render edilmesine yardımcı olurlar.

[Performansın iyileştirmesi](/docs/optimizing-performance.html#examples) yazısında  `shouldComponentUpdate()` fonksiyonunun ne olduğunu ve nasıl *pure component*'leri oluşturabileceğiniz hakkında bilgi edinebilirsiniz.

### Fonksiyon Component'leri {#function-components}

Square component'ini masıl **fonksiyon component**'i haline getireceğimize değinelim.

React'te **fonksiyon component**'leri sadece `render` metodunu içerdikleri ve state'leri bulunmadıkları için daha kolay bir şekilde component oluşturmayı sağlarlar. `React.Component`'tan türetilen bir sınıf oluşturmak yerine, sadece `prop`'ları girdi olarak alan ve neyin render edileceğini döndüren bir fonksiyon yazabiliriz. Fonksiyon component'leri kısa bir şekilde yazıldığı için, sınıf component'lerine göre sizi mental açıdan daha az yorar.

Square sınıfını aşağıdaki fonksiyon ile değiştirelim: 

```javascript
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

Kodda iki yerde `this.props` yerine `props` terimini kullandık.

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

>Not
>
>Square'i, fonksiyon component olarak değiştirerek aynı zamanda uzun olan `onClick={() => this.props.onClick()}` kod parçasını, `onClick={props.onClick}` şeklinde yazarak daha kısa hale getirmiş olduk (her iki taraftaki parantezlerin de gittiğine dikkat ediniz). Sınıf component'inde gerçek `this` değerine ulaşmak için arrow (ok) fonksiyonu kullanmıştık. Bunun tersine fonksiyon component'lerinde `this` ile uğraşmanıza gerek yoktur.

### Hamle Sırası Değişikliği {#taking-turns}

Şimdi tic-tac-toe oyunumuzdaki hatayı çözmemiz gerekiyor. Oyunun son hali ile sadece "X" eklenebiliyor ama "O" eklenemiyor.

Oyuna varsayılan olarak "X" başlıyor. X'in ilk başlayıp/başlamayacağını Board'un constructor'ındaki başlangıç state'inde belirleyebiliriz:

```javascript{6}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

Herhangi bir oyuncu hamlesini yaptığında `xIsNext` (xSonrakiElemanMı) boolean değişkeninin tersini alarak hangi oyuncunun sonraki hamleyi yapacağını belirleyebilir ve oyunun state'inde bunu kaydedebiliriz. Board'un `handleClick` fonksiyonunu, `xIsNext` değişkeninin zıttını dönüştürecek şekilde ilgili değişikliği yapalım:

```javascript{3,6}
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Bu değişiklik ile sayesinde, "X"'ler ve "O"'lar sırasıyla hamle yapabiliyor olacaklar. Ayrıca oyunda sıradaki hamlenin kimde olduğunu gösteren metni değiştirmek için Board'un, `render` metodunda "status" değişkenini oluşturabilirz:

```javascript{2}
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // Kalan kısımlar değişmedi
```

Bu değişikliklerden sonra Board component'inin son hali aşağıdaki gibi olacaktır:

```javascript{6,11-16,29}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)**

### Kazananın Belirlenmesi {#declaring-a-winner}

Artık sonraki oyuncuyu görüntüleyebiliyoruz. Bundan sonra artık oyunun bitmesi için oyunun kazanıldığını ve artık başka bir hamle kalmadığını göstermemiz gerekiyor. Bunun için, dosyanın sonuna yardımcı bir fonksiyon ekleyerek kazananı belirleyebiliriz:

```javascript
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

Board'un `render` fonksiyonunda, `calculateWinner(squares)`'ı çağırarak ilgili oyuncunun kazanma durumunu kontrol edebiliriz. Oyuncu kazandıysa, "Winner: X" veya "Winner: O" gibi kazananı belirten bir metin görüntüleyebiliriz. Şimdi, Board'un `render` fonksiyonunda yer alan `status` değişkenini aşağıdaki gibi değiştirelim:

```javascript{2-8}
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // geriye kalan kısımlar değiştirilmedi
```

Oyunda farkettiyseniz bir oyuncu, diğer oyuncunun işaretlediği karenin üstüne tekrar işaretleme yapabiliyor. Buna ek olarak oyun kazanıldığı durumda da tekrar hamle yapmayı engellemeliyiz. Bunun için Board'un `handleClick` fonksiyonunu ilgili koşullarda return edecek şekilde değiştirelim: 

```javascript{3-5}
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)**

Tebrikler! Artık çalışan bir tic-tac-toe oyununuz var. Ayrıca bu kısma kadar React'in temel özelliklerini de öğrenmiş durumdasınız. Bu nedenle aslında gerçek kazanan *sizsiniz*.

## Zamanda Yolculuğun eklenmesi {#adding-time-travel}

Son çalışma olarak oyunda önceki hamlelere gitmeyi sağayacak "zamanda geriye gitme" özelliğini ekleyelim.

### Hamlelerin Geçmişinin Saklanması {#storing-a-history-of-moves}

Eğer `squares` array'ine direkt olarak elle müdahale ederek değiştirseydik, zaman yolculuğu özelliğini geliştirmemiz daha zor olurdu.

Ancak, `slice()` fonksiyonu yardımıyla her hamleden sonra `squares` array'inin kopyasını alarak [immutable olarak değiştirilmesini sağladık](#why-immutability-is-important). Bu durum bize, `squares` array'inin geçmişteki her halinin kaydedebilmemize, ve halihazırda oluşan hamleler arasında gezinebilmemize imkan sağlamış oldu.

`squares` array'inin geçmiş hallerini tutabilmek için `history` adında bir array oluşturabiliriz. `history` array'i, oyundaki ilk hamleden son hamleye kadar oyun tahtasının tüm durumlarını aşağıdaki gibi tutuyor olacaktır: 

```javascript
history = [
  // İlk hamleden öncesi
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // İlk hamleden sonrası
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // İkinci hamleden sonrası
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```

Artık, hangi component'in state'inin `history` sahip olması gerektiğine karar vermemiz gerekiyor.

### State'in Ebeveyn Component'e Taşınması (Tekrar) {#lifting-state-up-again}

En üst seviyedeki Game component'inin, geçmiş hamlelerin listesini görüntülemesini istiyoruz. Bunun için, Game component'inin `history`'e erişebilmesi gerekiyor. Bunu sağlamanın yolu, `history`'i en üst seviyedeki Game component'ine taşımaktan geçiyor.

`history` state'ini, Game component'ine yerleştireceğimiz için, bir alt component olan Board'dan `squares` state'ini çıkarmamız gerekiyor. [lifted state up](#lifting-state-up)'ta Square component'inden Board component'ine yaptığımız gibi, şimdi de Board component'inden Game component'ine taşıma işlemini gerçekleştirmemiz gerekiyor. Bu sayede Game component'i, Board'un verisi üzerinde tamamen kontrolü ele almış olacak ve `history`'deki önceki hamlelerin Board'a işlemesini bildirebilecektir.

Öncelikle, Game component'inin constructor'ında, state'in ilk halini oluşturmamız gerekiyor: 

```javascript{2-10}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
    };
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

Şimdi Game component'inden Board component'ine `squares` array'ini `onClick` event'ini prop'lar aracılığıyla aktarmamız gerekiyor. Birden fazla Square için Board'da sadece bir tane click handler'ı bulunduğundan dolayı, tıklanan square'in hangisi olduğunun belirlenebilmesi için `onClick` handler'ına her bir Square'in konumunu iletmemiz gerekiyor. Bu gereksinimler için Board component'ini aşağıdaki gibi değiştirebilirsiniz: 

* Board'daki `constructor` siliniz.
* Board'un `renderSquare` metodunda `this.state.squares[i]` yerine `this.props.squares[i]` yazınız.
* Board'un `renderSquare` metodunda `this.handleClick(i)` yerine `this.props.onClick(i)` yazınız.

Board'un son hali aşağıdaki gibi olmalıdır:

```javascript{17,18}
class Board extends React.Component {
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.props.squares[i]}
        onClick={() => this.props.onClick(i)}
      />
    );
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

Şimdi de oyun geçmişindeki son girdiyi kullanarak, oyunun son durumunun belirlenmesi ve görüntülenmesi için, Game component'indeki `render` fonksiyonunu değiştirelim:

```javascript{2-11,16-19,22}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
```

Oyunun durumunu Game component'i render ettiği için, Board'daki `render` metodundan oyunun durumunu ilgilendiren kısımları çıkarabiliriz:

```js{1-4}
  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
```

Son olarak, Board component'indeki `handleClick` metodunu Game component'ine taşıyacağız. Ayrıca, Game component'i Board'a göre daha farklı oluşturulduğu için `handleClick` metodunu da uygun şekilde değiştirmemiz gerekiyor. Bunun için Game'in `handleClick` metodu içerisinde, oyundaki hamleleri `history` array'ine ekleyeceğiz:

```javascript{2-4,10-12}
  handleClick(i) {
    const history = this.state.history;
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares,
      }]),
      xIsNext: !this.state.xIsNext,
    });
  }
```

>Not
>
>Bir array'e eleman eklemek için genellikle array'in `push()` metodu kullanılır. Fakat `push()`'un aksine `concat()` metodu, orijinal array'i değiştirmez. Bu nedenle immutability'nin sağlanması için `concat()`fonksiyonunun kullanılması önem teşkil etmektedir.

Geldiğimiz noktada, Board component'i sadece `renderSquare` ve `render` metotlarına ihtiyaç duyuyor. Oyunun durumu ve `handleClick` metodu ise artık Game component'inde yer alıyor.

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### Geçmiş Hamlelerin Görüntülenmesi {#showing-the-past-moves}

tic-tac-toe oyununun geçmişini kaydedebildiğimize göre, artık oyuncuya geçmiş hamlelerin görüntülenmesini sağlayabiliriz. 

Daha önce React elemanlarının, birinci kalitede JavaScript nesneleri olduğunu öğrenmiştik. Bu sayede React elemanlarını, uygulama içerisinde istediğimiz yere aktarabiliyoruz. Bu nedenle JavaScript mantığıyla düşünerek, React'te birden fazla elemanı render edebilmek için, React elemanlarından oluşan bir array'i kullabiliriz.

JavaScript'te array'ler bir [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) (harita) metodu içerirler. Bu metod sayesinde verileri istenilen şekilde haritalayabilirler. Örneğin 1, 2, 3 sayılarının, iki katını alan bir dizinin oluşturulmasını sağlayabilirler:

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
``` 

`map` metodunu kullanarak oyunun hamle geçmişini, ekranda butonlar halinde görüntülemek için React elemanlarına map edebiliriz. Ve bu butonlara tıklayarak geçmiş hamlelere atlanmasını sağlayabiliriz.

Game'in `render` metodunda yer alan `history` array'i üzerinde `map` fonksiyonunun çalıştırılmasını sağlayalım: 

```javascript{6-15,34}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{moves}</ol>
        </div>
      </div>
    );
  }
```

**[Kodun bu kısma kadar olan son halini görüntülemek için tıklayınız](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)**

tic-tac-toe oyununun geçmişindeki her bir hamle için, `<button>` içeren bir `<li>` elemanı oluşturuyoruz. Butondaki `onClick` metodu, üzerine tıklandığında `this.jumpTo()` fonksiyonunu çağırıyor fakat henüz `jumpTo()` metodunu oluşturmadık. Şu an, oyun içerisinde oluşan hamlelerin bir listesini görüyor olmanız lazım. Ayrıca geliştirici araçları konsolunda da aşağıdaki şekilde bir uyarı vermiş olmalıdır:

>  Warning:
>  Each child in an array or iterator should have a unique "key" prop. Check the render method of "Game".

Üstteki uyarının ne anlama geldiğine bakalım.

### Key seçimi {#picking-a-key}

Bir liste görüntüledğimizde React, render edilen her bir liste elemanı için bazı bilgileri saklar. Listeyi güncellediğimizde React, listede neyin değiştiğine karar vermesi gerekir. Çünkü listenin elemanlarını eklemiş, silmiş, tekrar düzenlemiş veya güncellemiş olabilirirz. 

Listenin kodlarının buradan:

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

bu koda değiştiğini düşünelim: 

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

Bu iki kodu okuyan bir kişi, sayıların değişmesine ek olarak Alexa ile Ben'in sıralamasının değiştiğini, bununla birlikte Alexa ile Ben'in arasına Claudia'nın eklendiğini farkedecektir. Ancak React bir bilgisayar programıdır ve amacımızın ne olduğunu kestiremez. React uygulamada listeyi değiştirmemizdeki maksadımızın ne olduğunu bilemeyeceğindan dolayı, her liste eleamanını birbirinden ayırt etmek için, liste elemanlarına bir *key* (anahtar değer) vermemiz gerekir. Bu örnekte, `alexa`, `ben`, `claudia` ifadelerini key olarak kullanabilirz. Fakat bu verileri veritabanından getirseydik, key olarak Alexa, Ben, ve Claudia'nın ID'lerini kullanabilirdik:

```html
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

Bir liste tekrar render edileceği zaman React, her liste elemanının key'ini alır ve önceki listenin elemanlarıyla karşılaştırır. Eğer yeni listede, önceki listede bulunmayan bir key varsa React bir liste elemanı component'i oluşturur. Eğer önceki listede bulunan bir key, yeni listede bulunmuyorsa React, ilgili liste elemanını yok eder. Eğer iki key eşleşiyorsa, eski liste elemanı yeni listeye taşınır. React'in tekrar render etme aşamaları arasında state'in korunması amacıyla key'ler, her bir component'in kimliği hakkında React'e bilgi verir. Eğer bir component'in key'i değiştiyse, component React tarafından yok edilir ve yeni bir state ile tekrar oluşturulur.

React'teki `key` kelimesi özeldir ve React içerisinde rezerve edilmiş kelimeler arasındadır (`ref` de rezerve edilmiştir, fakat daha gelişmiş bir özelliktir). Bir eleman oluşturulduğunda React, elemanın `key` özellğini alır ve direkt olarak return edilen elemanın üzerinde saklar. `key` `props`'a ait gibi görünse de, `this.props.key` kullanılarak erişilemez. Çünkü `key` özelliği, React'in otomatik hangi component'i güncelleyeceğine karar vermesi için tasarlanmıştır. Bu nedenle bir component, kendi `key`'i hakkında bilgi edinemez.

**Dinamik listeler oluştururken, benzersiz key değerleri atamanız kesinlikle tavsiye edilir.** Eğer uygun key değerine sahip değilseniz, verinizi gözden geçirerek uygun bir id değerin bulmak mantıklı olacaktır. 

Eğer bir key ataması yapmazsanız, React bir uyarı görüntüler ve varsayılan olarak ilgili liste elemanının index'ini key olarak kullanır. Array'in index'ini key olarak kullanmak, liste elemanlarına ekleme/çıkarma veya tekrar sıralama yapılırken problem oluşturabilir. `key={i}` ataması yapmak uyarının susturulmasını sağlar ama array indeksleri üzerindeki problemi gidermez. Bu nedenle birçok durum için bu kullanım önerilmez. 

Key'lerin uygulama içerisinde global olarak benzersiz olmasına gerek yoktur. Sadece bulunduğu component'in içerisindeki diğer list elemanları arasında benzersiz olması gereklidir. 


### Implementing Time Travel {#implementing-time-travel}

In the tic-tac-toe game's history, each past move has a unique ID associated with it: it's the sequential number of the move. The moves are never re-ordered, deleted, or inserted in the middle, so it's safe to use the move index as a key.

In the Game component's `render` method, we can add the key as `<li key={move}>` and React's warning about keys should disappear:

```js{6}
    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li key={move}>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });
```

**[View the full code at this point](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)**

Clicking any of the list item's buttons throws an error because the `jumpTo` method is undefined. Before we implement `jumpTo`, we'll add `stepNumber` to the Game component's state to indicate which step we're currently viewing.

First, add `stepNumber: 0` to the initial state in Game's `constructor`:

```js{8}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  }
```

Next, we'll define the `jumpTo` method in Game to update that `stepNumber`. We also set `xIsNext` to true if the number that we're changing `stepNumber` to is even:

```javascript{5-10}
  handleClick(i) {
    // this method has not changed
  }

  jumpTo(step) {
    this.setState({
      stepNumber: step,
      xIsNext: (step % 2) === 0,
    });
  }

  render() {
    // this method has not changed
  }
```

We will now make a few changes to the Game's `handleClick` method which fires when you click on a square.

The `stepNumber` state we've added reflects the move displayed to the user now. After we make a new move, we need to update `stepNumber` by adding `stepNumber: history.length` as part of the `this.setState` argument. This ensures we don't get stuck showing the same move after a new one has been made.

We will also replace reading `this.state.history` with `this.state.history.slice(0, this.state.stepNumber + 1)`. This ensures that if we "go back in time" and then make a new move from that point, we throw away all the "future" history that would now become incorrect.

```javascript{2,13}
  handleClick(i) {
    const history = this.state.history.slice(0, this.state.stepNumber + 1);
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares
      }]),
      stepNumber: history.length,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Finally, we will modify the Game component's `render` method from always rendering the last move to rendering the currently selected move according to `stepNumber`:

```javascript{3}
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // the rest has not changed
```

If we click on any step in the game's history, the tic-tac-toe board should immediately update to show what the board looked like after that step occurred.

**[View the full code at this point](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### Wrapping Up {#wrapping-up}

Congratulations! You've created a tic-tac-toe game that:

* Lets you play tic-tac-toe,
* Indicates when a player has won the game,
* Stores a game's history as a game progresses,
* Allows players to review a game's history and see previous versions of a game's board.

Nice work! We hope you now feel like you have a decent grasp on how React works.

Check out the final result here: **[Final Result](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**.

If you have extra time or want to practice your new React skills, here are some ideas for improvements that you could make to the tic-tac-toe game which are listed in order of increasing difficulty:

1. Display the location for each move in the format (col, row) in the move history list.
2. Bold the currently selected item in the move list.
3. Rewrite Board to use two loops to make the squares instead of hardcoding them.
4. Add a toggle button that lets you sort the moves in either ascending or descending order.
5. When someone wins, highlight the three squares that caused the win.
6. When no one wins, display a message about the result being a draw.

Throughout this tutorial, we touched on React concepts including elements, components, props, and state. For a more detailed explanation of each of these topics, check out [the rest of the documentation](/docs/hello-world.html). To learn more about defining components, check out the [`React.Component` API reference](/docs/react-component.html).
