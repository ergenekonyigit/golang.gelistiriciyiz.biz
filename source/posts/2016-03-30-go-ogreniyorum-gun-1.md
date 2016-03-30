---
title: "Go öğreniyorum - Gün 1"
date: Mar 30, 2016 11:07
tags: go-ogreniyorum
subtitle: "`Introducing Go` kitabından bugün öğrendiklerim"
cover: golang-ogreniyorum-oreilly.jpg
---

Yaklaşık 1 ay’dır beklediğim siparişim geldi. O’Reilly’den satın aldığım
[Introducing Go](http://www.amazon.co.uk/dp/1491941952/ref=cm_sw_r_tw_dp_pe5-wb1E23MX7)
kitabını akşam eve gidince heyecanla okumaya başladım.READ_MORE

Öğrendiklerimi bu sitede paylaşacağım.

## Chapter 1

Mac OS X kullanıyorum ve [brew](http://brew.sh)’dan [Go](https://golang.org/)’yu 
kurmuştum kitaptan önce. Hemen ilk programa geçtim.

```go
package main

import "fmt"

// this is comment

func main() {
    fmt.Println("Hello, World")
}
```

Kitap bana şunu önerdi, hemen kendi bilgisayarınızda bir dizin oluşturun ve
bu kodu `example1.go` adıyla kaydedin:

```bash
mkdir -p ~/golang-book/chapter1
cd ~/golang-book/chapter1/
touch example1.go
```

Kullandığınız text editörüyle açın dosyayı, içine kodu ekleyin, kaydedin çıkın.
Daha sonra çalıştırmak için;

    go run example1.go

Eğer ekranda `Hello, World` çıktısını gördüyseniz işler yolundadır!

### Kodu Nasıl Okumalıyız ?

Go kodu, yukarıdan aşağı, soldan sağa, aynı kitap gibi okunur.

```go
package main
```

İlk satır **package declaration** olarak tanımlanır. Her Go programı mutlaka
bu tanımlamayla başlar. İki tür Go program tipi var: **Executable** ve **Library**. 
Executable olanlar direkt çalışan uygulamar (*komut satırından çalışan mesela*), 
Library ise kod koleksiyonlarından oluşan paketlerdir.

2.satır boş. Bilgisayarlar, bu tür boş satırları ve benzeri şeyleri özel
karakterlerle ifade ederler. **Newlines** (*yeni satırlar*), **Spaces** 
(*boşluk karakterleri*), **Tab** karakteri ve benzeri karakterlere 
**Whitespace** denir. Çünki bu karakterler insan gözüyle görüntülenmezler.

```go
import "fmt"
```

3. satır `import "fmt"`, başka birinin yaptığı paket içinden kodu alıp kendi
kodumuza eklemek içindir. Örneğin `fmt` paketi giriş/çıkış işlerini düzenler (I/O). Bu
mantıktan yola çıkınca, `fmt` paketi içinde acaba ilk satır ne olur du? tabiiki
`package fmt`

Go’da `string`'ler karakterler dizisi yani harfler, sayılar, semboller’den oluşur
ve belirli bir boyu olur. Çift tırnak içinde kullanılır.

```go
// this is comment
```

`//` ile başlayan satır, yorum satırıdır. Go derleyicisi bu satırları derleme
esnasında görmezden gelir. İki tür yorum şekli var. Satırsal ve bloksal. `//` ile
satırsal, `/* */` ile bloksal yorum (*comment*) yapılır.

```go
/* Bu satır
   Yorum satırı */
```

Bir satır boşluktan sonra **fonksiyon deklarasyonu**’nu görürsünüz:

```go
func main() {
    fmt.Println("Hello, World")
}
```

Fonksiyon, girdisi (**input**) çıktısı (**output**) ve sırayla çalışan ifadeleri 
(**statements**) bulunan şeydir. Tüm Go fonksiyonları `func` anahtar kelimesiyle
başlar ve bu kelimeyi fonksiyonun adı takip eder. Örnekte bu fonksiyonun adı: 
`main`. Ek olarak parantez içinde 0 ya da N tane parametre ve bazen opsiyonel
olarak fonksiyonun geriye döndürdüğü tip (**return type**) ve son olarak
süslü parantezlerle çevrelenmiş fonksiyonun gövdesi.

Örnek fonksiyon hiç parametre almıyor, hiçbir şey dönmüyor. `main` özel
bir durumda. Program çalışınca çağrılan fonksiyon bu.

```go
fmt.Println("Hello, World")
```

Son parçamız 3 bileşenden oluşuyor. Önce, `fmt` paketi içinden başka bir
fonksiyonu çağırıyoruz `Println` yani **print line** yani satırı yaz :) Daha
sonra içinde `Hello, World` yazan bir `string` oluşturuyoruz ve bunu parametre
olarak `Println` fonksiyonuna geçiyoruz ve fonksiyonu **invoke** ediyoruz yani
çalıştırıyoruz.

Bu kod’un en büyük ve esas işi yapan kısmı `Println` kısmı. Eğer tam olarak
neler yaptığını öğrenmek isterseniz:

    godoc fmt Println
    
    func Println(a ...interface{}) (n int, err error)
        Println formats using the default formats for its operands and writes to
        standard output. Spaces are always added between operands and a newline
        is appended. It returns the number of bytes written and any write error
        encountered.

Bu döküman derki;

> Println’a ne verirsen, standard output’a yollar!

Yani `Hello, World`’ün komut satırında görülmesi bu sayede oluyor.

## Chapter 2

### Types (Tipler)

Adı **Bıdık** olan bir kedin olsun. Tipi **Kedi**. Tüm kedilerin ortak özellikleri
var. Hepsinin **4 ayağı** var. Bu mantıkta, tüm kedilerin 4 ayağı var, Bıdık da
bir kedi, demekki Bıdığın da 4 ayağı var.

Tipler de aynı bu mantıkta çalışıyor. Tüm `string`’lerin boyu/uzunluğu var.
Eğer `x` bir `string` ise, mutlaka `length`’i de var demektir.

> Go statik olarak yazılan bir programlama dili!

Bu ne demek? değişkenlerin herzaman belirli bir tipi var ve bu tip 
**değiştirilemez**! Go pek çok veri tipi ile beraber geliyor.

### Numbers (Sayılar)

#### Integers

İki tür var: **integers** (*bildiğimiz sayılar*) ve **floating-point numbers** 
(*virgüllü sayılar*). Yani `-3, -2, 0, 1, 3, 4` gibi sayılar **10’luk** sayı sistemi
yani **decimal** sistemdir. Bilgisayar dünyasında kullandığımız sayı sistemi ise
**binary** yani **2’lik** sistemdir.

    1 1 0
    | | |
    | | +---------------- 0  [2^0 = 1]   (1.bit)
    | +------------------ 2  [2^1 = 2]   (2.bit)
    +-------------------- 4  [2^2 = 4]   (3.bit)
    
    0 + 2 + 4           = 6

**Integer** tipleri olarak `uint8`, `uint16`, `uint32`, `uint64`, `int8`, `int16`,
`int32` ve `int64` değerleri vardır. `8 16 32 64` gibi şeyler kaç bit kapasite
olduğunu belirtir. `uint` demek **unsigned integer**, `int` ise **signed integer**
anlamındadır.

> Unsigned Integer’lar sadece POZİTİF sayıları kapsar!

Ek olarak `byte` ve `rune` (*int32 ile aynı*) da vardır. `1 Byte = 8 bits` ve
alabileceği maksimum değer binary olarak `11111111` yani `255`’dir. İlave olarak
3 tane daha **machine dependent** yani derleyicinin üzerinde çalıştığı bilgisayara bağlı
olan tip var: `uint`, `int` ve `uintptr`.

Eğer normal sayılarla çalışacaksanız `int` kullanabilirsiniz :)

#### Floating-Point Numbers

En kolay ifadeyle ondalık sayılar: `1.5`, `0.25`, `3.14`. Virgül yerine **Nokta**
kullanıyoruz. Bu tür sayılarla çalışırken şunları unutmayın:

* Bazen doğru olmayan değerler olabilir. Örneğin: `1.01 - 0.99` sonucu normal
dünyada `0.02` olması gerekirken `0.020000000000000018` çıkar. (*Bu Ruby’de, Python’da 
da böyle.*)
* Integer’larda olduğunu gibi 32 bit ya da 64 bit gibi kesin bir boyutu vardır.
Büyük ölçekli ondalık sayılarla çalışınca hassiyet artabilir
* Bazen `NaN` (*not a number*, mesela 0/0 durumunda) ya da pozitif/negatif 
sonsuzluk durunlarında farklı sonuçlar gelebilir.

Go, 2 tane floating-point tipine sahip: `float32` ve `float64`. Kompleks
sayılar için de `complex64` ve `complex128` var. Önerilen `float64` ile
çalışmak (*gündelik işlerde*)

```go
package main

import "fmt"

func main() {
  fmt.Println("1 + 1 =", 1 + 1)
}
```

bunu `chapter2/example1.go` olarak kaydedip çalıştıralım:

```bash
cd ~/golang-book/chapter2/
go run example1.go
```

Sonuç : `1 + 1 = 2`. Yaptığımız işlemi özetlemek gerekirse:

1. sayısal kalıp `1` (*tipi: int*)
1. `+` operatörü (*toplama işini yapıyor*)
1. diğer sayısal kalıp (*numeric literal*) `1`

Şimdi şunu deniyelim:

```go
package main

import "fmt"

func main() {
  fmt.Println("1 + 1 =", 1.0 + 1.0)
}
```

bunu `chapter2/example2.go` olarak kaydedip çalıştıralım:

```bash
cd ~/golang-book/chapter2/
go run example2.go
```

Sonuç : `1 + 1 = 2` aynı... Matematik işlemlerinde;

* `+` : Toplama
* `-` : Çıkartma
* `*` : Çarpma
* `/` : Bölme
* `%` : Kalan (*Modulo*)

### Strings

Türkçesini bulamadım, harfsel, harf dizileri, karater dizesi gibi düşünebiliriz.
Çift tırnak ve **backtick** içinde kullanılabilir:

    "Hello World" # Çift tırnak (Double Quotes)
    `Hello World` # Backticks

> Çift tırnaklı string’ler çoklu satır içeremezler.

Bunu çözmek için `\n` ya da TAB için `\t` gibi **escape** karakterleri
kullanırlar;

```go
package main

import "fmt"

func main() {
  fmt.Println(len("Hello, World"))
  fmt.Println("Hello, World"[1])
  fmt.Println("Hello, " + "World")
  fmt.Println("This is line1\nLine 2")
  fmt.Println(`This is line1\nLine 2`)
}
```

bunu `chapter2/example3.go` olarak kaydedip çalıştıralım:

```bash
cd ~/golang-book/chapter2/
go run example3.go
```

Çıktıya baktığımızda;

```go
fmt.Println(len("Hello, World"))      // 12
fmt.Println("Hello, World"[1])        // 101
fmt.Println("Hello, " + "World")      // Hello, World
fmt.Println("This is line1\nLine 2")  // This is line1
                                      // Line 2
fmt.Println(`This is line1\nLine 2`)  // This is line1\nLine 2
```

olduğunu görürüz. Keza, string’leri karakter dizisi (**byte array**) olarak
düşünün. Aynı diğer dillerdeki gibi **0** index’li. Yani dizinin ilk
elemanı **0.** eleman. `fmt.Println("Hello, World"[1])` burada istediğimiz
`"Hello, World"` string’inin **1. elemanı** yani `e`. Gelen değer ise `101`
yani `e`’nin byte olarak karşılığı.

```go
fmt.Println("ABC"[0]) // 65
fmt.Println("ABC"[1]) // 66
fmt.Println("ABC"[2]) // 67
```

**string concatenation** yani string toplama/birleştirme işi aynı sayılardaki
gibi `+` ile oldu. `fmt.Println("Hello, " + "World")`

`fmt.Println("This is line1\nLine 2")` bu satırda `\n` ile **NEWLINE** yaptık.
Backticks içinde kullandığımız `\n` işlemedi.

### Booleans

`1-bit integer` yani `true` ya da `false`, `on` ya da `off`... Adını 
[George Boole](https://en.wikipedia.org/wiki/George_Boole)’dan alıyormuş :)
Kısaca mantıksal veri tipi.

    && : and (ve)
    || : or  (veya)
    !  : not (tersi ?)

şimdi örnek:

```go
package main

import "fmt"

func main() {
  fmt.Println(true && true)
  fmt.Println(true && false)
  fmt.Println(true || true)
  fmt.Println(true || false)
  fmt.Println(!true)
}
```

bunu `chapter2/example4.go` olarak kaydedip çalıştıralım;

```bash
cd ~/golang-book/chapter2/
go run example4.go
```

çıktı;

```go
fmt.Println(true && true)    // true
fmt.Println(true && false)   // false
fmt.Println(true || true)    // true
fmt.Println(true || false)   // true
fmt.Println(!true)           // false
```

Bu, bildiğimiz logic işlemler, yani tüm dillerde olan `and`, `or` ve `not`.

Evet... bugünlük bu kadar...