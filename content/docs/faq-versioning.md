---
id: faq-versioning
title: Sürümleme Politikası
permalink: docs/faq-versioning.html
layout: docs
category: FAQ
---

React [anlamsal sürümleme (semver)](https://semver.org/lang/tr/) prensiplerini uygulamaktadır.

Bu demektir ki sürüm numarası **x.y.z** ile:

* **Uyumsuz değişiklikleri** yayınlarken **x** değerini güncelleyerek  **ana sürümü** yayınlarız  (Örneğin: 15.6.2'den 16.0.0'a geçiş).
* **Yeni özellikleri** yayınlarken **y** değerini güncelleyerek **minör sürümü** yayınlarız (Örneğin: 15.6.2'den 15.7.0'a geçiş).
* **Hata düzeltmelerini** yayınlarken **z** değerini güncelleyerek **yama sürümünü** yayınlarız (Örneğin: 15.6.2'den 15.6.3'a geçiş).

Ana sürümler de yeni özellikler içerebilir, ve herhangi bir yeni sürüm hata düzeltmelerini bulundurabilir.

### Uyumsuz Değişiklikler {#breaking-changes}

Uyumsuz değişiklikler hepimiz için zahmetli olduğu için ana sürümlerin sayısını olabildiğince az tutmaya çalışıyoruz – örneğin, React 15, Nisan 2016'da, React 16, Eylül 2017'de yayınlanmıştır; React 17'nin 2019'dan önce yayınlanması beklenmemektedir.

Bunun yerine yeni özellikleri minör sürümlerle yayınlamaktayız. Bu nedenle minör sürümler çoğu zaman ana sürümlerden daha ilgi çekici ve merak uyandırıcı olmaktadır.

### Kararlılığa Bağlılık {#commitment-to-stability}

React'ı zaman içinde değiştirdikçe React'ın yeni özelliklerindan faydalanmak için gereken çabayı azaltmaya özen göstermekteyiz.
Bir önceki APIyi başka pakete koymamız gerekse bile, eski APIyi olabildiğince çalışır durumda tutarız. Örneğin, [mixinlerin kullanımı yıllardır tavsiye edilmese bile](/blog/2016/07/13/mixins-considered-harmful.html), mixinler bu zamana kadar [create-react-class ile](/docs/react-without-es6.html#mixins) desteklenmiştir ve birçok proje mixinleri eski kodlarında stabil şekilde kullanmaya devam etmektedir.

React kullanan bir milyondan fazla geliştirici, milyonlarca React bileşenini devam ettirmektedir. Sadece Facebook'un kodunda 50.000'den fazla React bileşeni vardır. Bu nedenle React versiyon yükseltemelerini olabildiğince kolay hale getirmemiz gerekmektedir; eğer büyük değişikler yapar ve buna geçiş için bir yol haritası sunmazsak, geliştiriciler eski sürümlerde takılı kalırlar. Geçiş için sunduğumuz çözümleri Facebook'ta kendimiz de test etmekteyiz - eğer 10 kişiden az olan takımımız, 50.000'den fazla bileşeni güncelleyebiliyorsa, React kullanan herkesin bu geçişi kolaylıkla yapabileceğine inanıyoruz. Çoğu zaman  [otomatikleştirilmiş scriptlerle](https://github.com/reactjs/react-codemod) bileşenleri güncelliyoruz, ve sonrasında bunları herkesin kullanması için açık kaynak sürümümüze dahil ediyoruz.

### Uyarılarla Kademeli Versiyon Geçişi {#gradual-upgrades-via-warnings}

React'ın geliştirme derlemeleri birçok yararlı uyarı içerir. Uyumsuz değişikliklere hazırlık için olabildiğince uyarı eklemekteyiz. Bu sayede, eğer uygulamanız son sürümde herhangi bir uyarı içermiyorsa, sonraki ana sürüme uyumlu olacaktır. Bu size uygulamalarınızdaki bileşenleri teker teker yeni sürüme geçirme olanağı sağlar.

Geliştirme uyarıları uygulamanızın işleyişini değiştirmez. Bu sayede uygulamanızın geliştirme ve canlı ortam derlemelerinde aynı şekilde davranacağına emin olabilirsiniz; aradaki tek fark canlı ortam derlemesinin uyarıları loglamayacak olmasıdır, ki bu daha verimlidir. (Eğer aksini farkederseniz, lütfen sorunu paylaşın)

### Neler Uyumsuz Değişikliklerdir? {#what-counts-as-a-breaking-change}

Aşağıdaki durumlarda genellikle ana versiyon yükseltmesi *yapmıyoruz*:

* **Geliştirme uyarıları.** Bunlar canlı ortamın davranışını etkilemediği için yeni uyarıları ekleyebilir, ya da varolanları değiştirebiliriz. Bu aslında gelecek uyumsuz değişikliklere karşı geliştiricileri güvenilir biçimde uyarmamızı sağlamaktadır.
* **`unstable_` ile başlayan APIler.** Bunlar APIlerinden henüz emin olunmayan deneysel özelliklerdir. Bunları `unstable_` ile başlayacak şekilde yayınlayarak daha hızlı ilerleyebilmekte ve stabil APIyi daha önce sunabilmekteyiz.
* **React'ın alfa ve kanarya sürümleri.** Yeni özelliklerin daha önce test edilebilmesi için alfa sürümlerini sunmaktayız, fakat alfa sürümünden öğrendiklerimizle de değişiklik yapma esnekliğine ihtiyaç duyuyoruz. Bu versiyonları kullanıyorsanız, APIlerin stabil sürümden önce değişebileceği ihtimalini unutmayın.
* **Dökümente edilmemiş APIler ve içsel veri yapıları.** Eğer `__SECRET_INTERNALS_DO_NOT_USE_OR_YOU_WILL_BE_FIRED` ya da `__reactInternalInstance$uk43rzhitjg`, gibi dahili özellik isimlerine erişim sağladığınızda hiçbir güvence yoktur. Bu noktada artık kendi başınızasınız.

Bu prensipler faydacı yaklaşımla tasarlanmıştır; kesinlikle sizler için baş ağrısına sebep olmak istemiyoruz. Eğer bütün bu değişiklerle ana versiyon çıkarsak, daha fazla sayıda ana versiyon çıkmış oluruz ve bu topluluğa daha fazla versiyon çilesi yaratır. Ayrıca bu durum React'ı geliştirmek ve ilerletmek için istediğimiz kadar hızlı olamayacağımız anlamına da gelir.

Bununla beraber, eğer bu listedeki bir değişikliğin toplulukta fazlaca sorun yaratacağını düşünüyorsak, kademeli geçişte yol haritası sunmak için elimizden gelenin en iyisini yapmaya özen gösteriyoruz. 