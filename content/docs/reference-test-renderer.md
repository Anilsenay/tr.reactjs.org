---
id: test-renderer
title: Test Render Edici
permalink: docs/test-renderer.html
layout: docs
category: Reference
---

**Importing**

```javascript
import TestRenderer from 'react-test-renderer'; // ES6
const TestRenderer = require('react-test-renderer'); // ES5 with npm
```

## Genel Bakış {#overview}


Bu paket, DOM'a veya yerel bir mobil ortama bağlı olmadan React bileşenlerini saf JavaScript objesine  dönüştürmek için kullanılabilecek bir React render edici sağlar.

Temel olarak, bu paket, bir tarayıcı veya [jsdom] (https://github.com/tmpvar/jsdom) kullanmadan, React DOM veya React Native bileşeninin oluşturduğu platform görünümü hiyerarşisinin (DOM ağacına benzer olarak) anlık görüntüsünü almayı kolaylaştırır.

Örnek:

```javascript
import TestRenderer from 'react-test-renderer';

function Link(props) {
  return <a href={props.page}>{props.children}</a>;
}

const testRenderer = TestRenderer.create(
  <Link page="https://www.facebook.com/">Facebook</Link>
);

console.log(testRenderer.toJSON());
// { type: 'a',
//   props: { href: 'https://www.facebook.com/' },
//   children: [ 'Facebook' ] }
```

<<<<<<< HEAD
JSON ağacının bir kopyasını bir dosyaya otomatik olarak kaydetmek ve testlerinizde değişip değişmediğini kontrol etmek için Jest'in anlık görüntü test özelliğini kullanabilirsiniz [Daha fazla bilgi için](https://facebook.github.io/jest/blog/2016/07/27/jest-14.html).


Ayrıca bileşen çıktısı üzerinde gezerek, belirli düğümleri bulup bu düğümler üzerinde doğrulama metotlarını (toBe, toEqual vb.) çağırabilirsiniz:
=======
You can use Jest's snapshot testing feature to automatically save a copy of the JSON tree to a file and check in your tests that it hasn't changed: [Learn more about it](https://jestjs.io/docs/en/snapshot-testing).
>>>>>>> 899411236d5b1520ab8b8e7fad7d48c681abc69b


```javascript
import TestRenderer from 'react-test-renderer';

function MyComponent() {
  return (
    <div>
      <SubComponent foo="bar" />
      <p className="my">Merhaba</p>
    </div>
  )
}

function SubComponent() {
  return (
    <p className="sub">Sub</p>
  );
}

const testRenderer = TestRenderer.create(<MyComponent />);
const testInstance = testRenderer.root;

expect(testInstance.findByType(SubComponent).props.foo).toBe('bar');
expect(testInstance.findByProps({className: "sub"}).children).toEqual(['Sub']);
```

### Test Renderer {#testrenderer}

* [`TestRenderer.create()`](#testrenderercreate)

### TestRenderer Nesnesi {#testrenderer-instance}

* [`testRenderer.toJSON()`](#testrenderertojson)
* [`testRenderer.toTree()`](#testrenderertotree)
* [`testRenderer.update()`](#testrendererupdate)
* [`testRenderer.unmount()`](#testrendererunmount)
* [`testRenderer.getInstance()`](#testrenderergetinstance)
* [`testRenderer.root`](#testrendererroot)

### Test Nesnesi {#testinstance}

* [`testInstance.find()`](#testinstancefind)
* [`testInstance.findByType()`](#testinstancefindbytype)
* [`testInstance.findByProps()`](#testinstancefindbyprops)
* [`testInstance.findAll()`](#testinstancefindall)
* [`testInstance.findAllByType()`](#testinstancefindallbytype)
* [`testInstance.findAllByProps()`](#testinstancefindallbyprops)
* [`testInstance.instance`](#testinstanceinstance)
* [`testInstance.type`](#testinstancetype)
* [`testInstance.props`](#testinstanceprops)
* [`testInstance.parent`](#testinstanceparent)
* [`testInstance.children`](#testinstancechildren)

## Başvuru Dokümanı {#reference}

### `TestRenderer.create()` {#testrenderercreate}

```javascript
TestRenderer.create(element, options);
```

İletilen React elemanı ile bir TestRenderer nesnesi oluşturun. Bu nesne gerçek DOM'u kullanmaz; ancak yine de bileşen ağacını tamamen belleğe render eder, böylece bu konuda doğrulamalar (assertions) yapabilirsiniz. Döndürülen nesne, aşağıda belirtilen metot ve özelliklere sahiptir:

### `testRenderer.toJSON()` {#testrenderertojson}

```javascript
testRenderer.toJSON()
```

İşlenen ağacı temsil eden bir nesne döndürün. Bu ağaç yalnızca <div> veya <View> gibi platforma özgü birimleri ve bunların bileşenlerini içerir, ancak kullanıcı tarafından yazılmış bileşenleri içermez.Bu, anlık görüntü [snapshot](https://facebook.github.io/jest/docs/en/snapshot-testing.html#snapshot-testing-with-jest) testi için kullanışlıdır.

### `testRenderer.toTree()` {#testrenderertotree}

```javascript
testRenderer.toTree()
```

Render edilen ağacı temsil eden bir nesne döndürün. `toJSON()` 'dan farklı olarak, gösterim `toJSON()` tarafından sağlanandan daha fazla ayrıntıya sahiptir ve kullanıcı tarafından yazılan bileşenleri içerir. Test render ediciye ilave olarak kendi doğrulama kütüphanenizi yazmadığınız sürece muhtemelen bu yönteme ihtiyacınız olmayacaktır.

### `testRenderer.update()` {#testrendererupdate}

```javascript
testRenderer.update(element)
```

Dahili bellek ağacını yeni bir kök elemanla tekrar render edin. Bu, kökte bir React güncellemesini simüle eder. Yeni eleman, önceki elemanla aynı tip ve anahtara sahipse, ağaç güncellenir; aksi takdirde yeni bir ağaca yeniden monte edilir.

### `testRenderer.unmount()` {#testrendererunmount}

```javascript
testRenderer.unmount()
```

Uygun yaşam döngüsü olaylarını tetikleyerek dahili hafıza ağacını çıkarın.

### `testRenderer.getInstance()` {#testrenderergetinstance}

```javascript
testRenderer.getInstance()
```

Eğer mevcutsa, kök elemana karşılık gelen nesneyi döndürün. Kök eleman eğer bir fonksiyon bileşeni ise, bir nesnesi olmadığından çalışmaz.

### `testRenderer.root` {#testrendererroot}

```javascript
testRenderer.root
```

Ağaçtaki belirli düğümler hakkında doğrulama yapmaya yarayan kök "test nesnesini" döndürür. Aşağıda daha derinde bulunan diğer "test nesnelerini" bulmak için kullanabilirsiniz.

### `testInstance.find()` {#testinstancefind}

```javascript
testInstance.find(test)
```

`test(testInstance)` 'ı `true` olarak döndüren tek bir alt test nesnesi bulun. Eğer bir test nesnesi için `test(testInstance)` `true` döndürmez ise, bir hata verecektir.

### `testInstance.findByType()` {#testinstancefindbytype}

```javascript
testInstance.findByType(type)
```

Verilen `type` ile tek bir alt test nesnesi bulun. Verilen `type` ile tam bir test nesnesi yoksa, bir hata verecektir.


### `testInstance.findByProps()` {#testinstancefindbyprops}

```javascript
testInstance.findByProps(props)
```

Verilen prop'lara sahip olan bir alt test nesnesi bulun. Tam olarak verilen prop'lara sahip bir test nesnesi yoksa, bir hata verecektir.

### `testInstance.findAll()` {#testinstancefindall}

```javascript
testInstance.findAll(test)
```

`test(testInstance)`'ı `true` olarak döndüren tüm alt test nesnelerini bulun.

### `testInstance.findAllByType()` {#testinstancefindallbytype}

```javascript
testInstance.findAllByType(type)
```

Verilen `type` ile tüm alt test nesnelerini bulun.


### `testInstance.findAllByProps()` {#testinstancefindallbyprops}

```javascript
testInstance.findAllByProps(props)
```

Verilen `prop`'lara ile tüm alt test nesnelerini bulun.

### `testInstance.instance` {#testinstanceinstance}

```javascript
testInstance.instance
```

Bu test nesnesine karşılık gelen bileşen nesnesi. Fonksiyon bileşenlerinin nesneleri bulunmadığından yalnızca sınıf bileşenleri için kullanılabilir. Verilen bileşenin içindeki `this` değerine karşılık gelir.

### `testInstance.type` {#testinstancetype}

```javascript
testInstance.type
```

Bu test nesnesine karşılık gelen bileşen türü. Örneğin, bir `<Button />` bileşeni bir tür `Button` türüne sahiptir.

### `testInstance.props` {#testinstanceprops}

```javascript
testInstance.props
```

Bu test nesnesine karşılık gelen prop'lar. Örneğin, bir `<Button size ="small"/>` bileşeni props olarak `{size: 'small'}` 'a sahiptir.

### `testInstance.parent` {#testinstanceparent}

```javascript
testInstance.parent
```

Bu test nesnesinin üst test örneği.


### `testInstance.children` {#testinstancechildren}

```javascript
testInstance.children
```

Bu test objesinin alt test nesneleri.


## Öneriler {#ideas}

`createNodeMock` fonksiyonunu, özel taklit referanslarına izin veren seçenek olarak“TestRenderer.create” 'e iletebilirsiniz. `createNodeMock`, mevcut elemanı kabul eder ve taklit olan bir başvuru nesnesi return eder. Bu, referanslara dayanan bir bileşeni test ederken kullanışlıdır.

```javascript
import TestRenderer from 'react-test-renderer';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.input = null;
  }
  componentDidMount() {
    this.input.focus();
  }
  render() {
    return <input type="text" ref={el => this.input = el} />
  }
}

let focused = false;
TestRenderer.create(
  <MyComponent />,
  {
    createNodeMock: (element) => {
      if (element.type === 'input') {
        // mock a focus function
        return {
          focus: () => {
            focused = true;
          }
        };
      }
      return null;
    }
  }
);
expect(focused).toBe(true);
```
