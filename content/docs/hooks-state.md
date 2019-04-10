---
id: hooks-state
title: State Hook kullanımı
permalink: docs/hooks-state.html
next: hooks-effect.html
prev: hooks-overview.html
---

*Hook'lar* React 16.8. ile gelen yeni bir eklentidir. Bu yeni eklenti size herhangi bir sınıf oluşturmadan state ve diğer React özelliklerini kullanmaya izin verir.

[önceki sayfada](/docs/hooks-intro.html) Hook'lara aşağıdaki örnekle bir giriş yapılmıştı:

```js{4-5}
import React, { useState } from 'react';

function Example() {
  // count adında yeni bir state değişkeni tanımlandı.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Şimdi Hook'ları öğrenmeye bu Hook kodu ile bu koda eşdeğer sınıf kodunu karşılaştırarak başlıyoruz. 

## Eşdeğer Sınıf Örneği {#equivalent-class-example}

Eğer React'da sınıfları kullandıysanız, Bu kod size tanıdık gelecektir.

```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

State `{ count: 0 }` olarak başlar ve kullanıcı her tıkladığında `this.setState()` çağırılarak `state.count` arttırılır. Sayfa boyunca bu sınıftan parçalar kullanacağız.


>Not
>
>Neden daha gerçekçi bir örnek yerine sayaç kullandığımızı merak ediyor olabilirsiniz. Bu, Hook'lar ile ilk adımlarınızı atarken API'ye odaklanmanıza yardımcı olacaktır. 

## Hook'lar ve Fonksiyon Bileşenleri {#hooks-and-function-components}

React'daki fonksiyon bileşenlerinin böyle gözüktüğünü unutmayınız:

```js
const Example = (props) => {
  // Hook'ları burada kullanabilirsiniz!
  return <div />;
}
```

ya da bunu:

```js
function Example(props) {
  // Hook'ları burada kullanabilirsiniz!
  return <div />;
}
```

Yukarıdakileri "stateless bileşenler" olarak biliyor olabilirsiniz. Şimdi bunlarla React state kullanma yeteneğini açıklıyoruz ve bu yüzden bunlara "fonksiyon bileşenleri" demeyi tercih ediyoruz. 

Hook'lar sınıfların içinde **çalışmazlar** fakat onları sınıf yazmadan da kullanabilirsiniz.

## Hook Nedir? {#whats-a-hook}

Yeni örneğimize React'dan `useState` hook'u import etmekle başlıyoruz

```js{1}
import React, { useState } from 'react';

function Example() {
  // ...
}
```

**Hook Nedir?** Hook React özelliklerini "bağlayabilmemize" izin veren özel bir fonksiyondur. Örneğin `useState`,  React state'i fonksiyon bileşenlerine eklememize izin veren bir Hook'tur. Yakında diğer Hook'ları da öğreneceğiz.


**Ne zaman hook kullanmalıyım?** Eğer bir fonksiyon yazar ve bunu gerçeklemek isterseniz, bazı state'leri eklemeniz gerekiyor. Önceden bunu sınıfa çevirmeniz gerekiyordu fakat şimdi mevcut fonksiyon bileşenlerinin içinde Hook kullanabilirsiniz.


>Not:
>
>Hook'ları bileşenlerlerin içinde kullanıp kullanamayacağımız hakkında birkaç özel kural vardır. Bunları [Rules of Hooks](/docs/hooks-rules.html) burada öğreneceğiz.


## State Değişkeni Tanımlanması  {#declaring-a-state-variable}

sınıfta `count` state'ini constructor (yapıcı fonksiyon) içinde `this.state`'i `{ count: 0 }`'a eşitleyerek `0` olarak başlatıyoruz. 

```js{4-6}
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
```

fonksiyon bileşenlerinde `this` yoktur bu yüzden `this.state` değer ataması veya okuma yapamıyoruz. Bunun yerine bileşenimizin içinde direkt olarak `useState` hook'unu çağırıyoruz. 

```js{4,5}
import React, { useState } from 'react';

function Example() {
  // "count" adında yeni bir state değişkeni tanımlıyoruz.
  const [count, setCount] = useState(0);
```

**`useState`'i çağırmak ne işe yarar?** Bu yeni bir "state değişkeni" tanımlar. Değişkenimizin adı `count` fakat farklı bir şekilde çağırabiliriz örneğin `banana`. Bu yöntemle fonksiyon çağrıları arasında verilerinizi koruyabilirsiniz. — `useState` ise `this.state`'in sınıfta sağladığı özellikleri kullanmanın yeni bir yoludur. Normalde değikenler fonksiyon bitiminde kaybolur fakat state değişkenleri React tarafından korunur.

**`useState`'e argüman olarak ne atarız?** `useState()` Hook için tek argüman initial (başlangıç) state argümanıdır. Sınıfların aksine, state, nesneye sahip olmak zorunda değildir. Sayı ya da string tutabiliriz. Örneğimizde kullanıcının tıklama sayısı için bir sayı istedik bu yüzden değişkenimizin başlangıç değeri `0` olarak atandı. (eğer state'in içinde iki farklı tutmak isteseydik,  `useState()`'i iki kere çağırmamız gerekecekti.)

**`useState` geriye ne döndürür?** `useState` geriye iki tane değer döndürür: şimdiki state ve güncelleyen fonksiyon. Bu, `const [count, setCount] = useState()` yazmamızın sebebidir. Bu, bir sınıftaki `this.state.count` ve `this.setState`'e benzer. Eğer bizim kullandığımız söz dizimi size tanıdık değilse, bunun için geri döneceğiz. [bu sayfanın alt kısmında](/docs/hooks-state.html#tip-what-do-square-brackets-mean).

Şimdi `useState` Hook'un ne olduğunu biliyoruz, örneğimiz daha anlamlı olacak.

```js{4,5}
import React, { useState } from 'react';

function Example() {
  // "count" adında yeni bir state değişkeni tanımlıyoruz.
  const [count, setCount] = useState(0);
```


`count` adında state değişkeni tanımladık ve `0`'a eşitledik. React, yeniden render edilenler arasındaki mevcut değerini hatırlayacak ve fonksiyonumuza en yeni değeri verecektir. Eğer şuanki `count` değerini değiştirmek isterseniz  `setCount` çağırabilirsiniz.


>Not
>
>`useState` 'in isminin neden `createState` olmadığını merak ediyor olabilirsiniz.
>
>"Create" oldukça doğru olmazdı çünkü state, sadece ilk kez bileşenimizi render ettiğimizde oluşturulur. Sonraki renderlarda `useState` bize o anki state'i verir. Aksi takdirde bu "state" olmazdı. Aynı zamanda hook'ların isimlerinin neden *hep* `use` ile başlamasının nedeni de var. Bunu daha sonra [Rules of Hooks](/docs/hooks-rules.html) bölümünde öğreneceğiz.

## State Okuma {#reading-state}

Geçerli count'u göstermek istediğimiz zaman `this.state.count`'i okuruz:

```js
  <p>You clicked {this.state.count} times</p>
```

In a function, we can use `count` directly:


```js
  <p>You clicked {count} times</p>
```

## State Güncelleme {#updating-state}

`count` state'i güncellemek için sınıfın içinde `this.setState()`'i çağırmamız gerekiyor.

```js{1}
  <button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
  </button>
```

Fonksiyonda zaten değişken olarak `setCount` ve `count`'a sahibiz, bu yüzden `this`'e ihtiyaç duymuyoruz :

```js{1}
  <button onClick={() => setCount(count + 1)}>
    Click me
  </button>
```

## Özet {#recap}

Hadi şimdi **öğrendiklerimizi baştan sona özetleyelim**

<!--
  I'm not proud of this line markup. Please somebody fix this.
  But if GitHub got away with it for years we can cheat.
-->
```js{1,4,9}
 1:  import React, { useState } from 'react';
 2:
 3:  function Example() {
 4:    const [count, setCount] = useState(0);
 5:
 6:    return (
 7:      <div>
 8:        <p>You clicked {count} times</p>
 9:        <button onClick={() => setCount(count + 1)}>
10:         Click me
11:        </button>
12:      </div>
13:    );
14:  }
```

* **Line 1:** React'dan `useState` Hook'u ekliyoruz. Bu yerel state'i fonksiyon bileşenlerinde tutmamıza izin verecek
* **Line 4:** `Example` bileşeninin içinde `useState` Hook'u çağırarak yeni bir state değişkeni tanımlıyoruz. Bu isimlerini bizim verdiğimiz bir çift değer döndürür. Değişkenimizin adı `count` çünkü tıklama sayısını tutuyor.`useState`e `0` yollayarak `count`'u `0`sıfırdan başlatıyoruz. İkinci döndürülen değerin kendisi bir fonksiyondur. Bu, bize `count`'u güncellemek için izin verir. bu yüzden onu `setCount` diye isimlendirdik.
* **Line 9:** Kullanıcı her tıkladığında, `setCount`'u yeni bir değerle çağırırız. React, `Example` bileşenini tekrar render edip, ona yeni `count` değerini atar.

Başlarken, eklenecek çok şey varmış gibi gözükebilir. Acele etmeyin! Açıklamalar arasında kaybolduysanız, yukarıdaki koda tekrar bakın ve baştan sona tekrar okumaya çalışın. State'in sınıfta nasıl çalıştığını unuttuğunda, bu koda meraklı gözlerle tekrar bak.Sana söz veriyoruz kod anlamlı gelecek.


### İpucu: Köşeli Parantez Ne Anlama gelir? {#tip-what-do-square-brackets-mean}

State değişkenlerini tanımlarken köşeli parantezleri fark etmiş olabilirsiniz:

```js
  const [count, setCount] = useState(0);
```

Soldaki isimler React API'ın bir parçası değiller. State değişkeninizi adlandırabilirsiniz:

```js
  const [fruit, setFruit] = useState('banana');
```

Bu JavaScript sözdiziminin adı ["array destructuring"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring). Bunun anlamı `fruit` ve `setFruit` diye iki yeni değişken oluştururken, `fruit`'in yazıldığı yer, ilk değer, `useState` döndürür ve `setFruit`, ikinci, bu koda eşittir: 


```js
  var fruitStateVariable = useState('banana'); // Returns a pair
  var fruit = fruitStateVariable[0]; // First item in a pair
  var setFruit = fruitStateVariable[1]; // Second item in a pair
```

`useState` ile state değişkeni tanımladığımız zaman, bu bir çift (iki elemanlı bir dizi) döndürür. İlk eleman o anki değer, ikincisi ise onu güncelleyen fonksiyondur. `[0]` ve `[1]` kullanarak erişmek biraz kafa karıştırıcı çünkü onların kendine özgü anlamları var. Bu yüzden dizi yıkıcıların yerine kullanıyoruz.

>Not
>
>React'ın `useState` bileşenlerinin hangi bileşene karşılık geldiğini nasıl anladığını merak ediyor olabilirsiniz. çünkü `this` gibi bir şeyi React'a göndermedik. Bunu burada cevaplıyoruz: [this question](/docs/hooks-faq.html#how-does-react-associate-hook-calls-with-components) ve birçok şeyi FAQ bölümünde cevaplıyoruz.

### İpucu: Çoklu State Değişkeni Kullanımı {#tip-using-multiple-state-variables}

State değişkeni tanımlarken bir çift `[something, setSomething]` kullanışlıdır çünkü birden fazla kullanmak istersek *farklı* isimleri farklı state değişkenlerine verebiliriz.

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
```

Yukarıdaki bileşende, `age`, `fruit` ve `todos`'a yerel değişken olarak sahibiz ve bunları teker teker güncelleyebiliriz.

```js
  function handleOrangeClick() {
    // Similar to this.setState({ fruit: 'orange' })
    // bu this.setState({ fruit: 'orange' })'a benzer.
    setFruit('orange');
  }
```

You **don't have to** use many state variables. State variables can hold objects and arrays just fine, so you can still group related data together. However, unlike `this.setState` in a class, updating a state variable always *replaces* it instead of merging it.
bir çok state değişken **kullanmak zorunda değilsiniz**. State değişkenleri, objeler ve dizileri çok iyi tutabilr bu yüzden ilgili verileri birlikte tutabilirsiniz fakat sınıftaki `this.setState`'ın aksine state değişkenini güncellemek birleştirmek(merge) yerine *değiştirir*.

Bağımsız değişkenleri bölme konusunda daha çok fazla öneriye bu bölümden ulaşabilirsiniz [in the FAQ](/docs/hooks-faq.html#should-i-use-one-or-many-state-variables).


## Sonraki Adımlar {#next-steps}

Biz Bu sayfada React tarafından sağlanan Hook'lardan birini, `useState`'i, öğrendik. Bazen buna "State Hook" dedik. Bu bizim React fonksiyon bileşenlerine yerel state eklememize izin veriyor. -- Şimdiye kadar ilk defa yaptık!

Aynı zamanda Hook'lar hakkında bir şeyler öğrendik. Hook'lar foksiyon bileşenlerinden özellikleri React'a bağlamanıza izin verirler. İsimleri her zaman `use` ile başlar ve henüz öğrenmediğimiz Hook'lar var.


**Hadi şimdi şununla devam edelim [learning the next Hook: `useEffect`.](/docs/hooks-effect.html)** Bu, bileşenlere yan etkiler yapmaya izin verir ve sınıflardaki lifecycle fonksiyonlarına benzer
