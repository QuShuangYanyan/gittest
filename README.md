尽管DOM作为API已经非常完善了，但是为了实现更多的功能，DOM仍然进行了扩展，其中一个重要的扩展就是对选择器API的扩展。人们对jQuery的称赞，很多是由于jQuery方便的元素选择器。除了前面已经介绍过的getElementsByClassName()方法外，DOM拓展了querySelectorAll()、querySelector()和matchesSelector()这3种方法，通过CSS选择符查询DOM文档取得元素的引用的功能变成了原生的API，解析和树查询操作在浏览器内部通过编译后的代码来完成，极大地改善了性能。本文将详细介绍html5新增的3种selector方法

querySelector() [注意]IE7-浏览器不支持

　　方法接收一个CSS选择符，返回与该模式匹配的第一个元素，如果没有找到匹配的元素，返回null。该方法既可用于文档document类型，也可用于元素element类型。关于CSS选择器的详细内容移步至此。
  
querySelectorAll()[注意]IE7-浏览器不支持

　　接收一个CSS选择符，返回一个类数组对象NodeList的实例。具体来说，返回的值实际上是带有所有属性和方法的NodeList，而其底层实现则类似于一组元素的快照，而非不断对文档进行搜索的动态查询。这样实现可以避免使用NodeList对象通常会引起的大多数性能问题。只要传给querySelectorAll()方法的CSS选择符有效，该方法都会返回一个NodeList对象，而不管找到多少匹配的元素

　　没有匹配元素时，返回空的类数组对象，而不是null。
  
matchesSelector() [注意]一般地，使用matches()方法来替代matchesSelector()方法

　　 方法接收一个CSS选择符参数，如果调用元素与该选择符相匹配，返回true；否则返回false
  
  非实时
        与getElementById()和getElementsByTagName()方法不同，querySelector()和querySelectorAll()方法得到的类数组对象是非动态实时的
  缺陷
　   　selector类方法在元素上调用时，指定的选择器仍然在整个文档中进行匹配，然后过滤出结果集，以便它只包含指定元素的后代元素。这看起来是违反常规的，因为它意味着选择器字符串能包含元素的祖先而不仅仅是所匹配的元素 
  
  按照正常理解，控制台应该返回空的类数组对象，因为id为container的div元素的子元素中，不存在div元素嵌套的情况

　　但是，该方法实际返回[div div]。这是因为参数中的选择器包含了元素的祖先

　　所以，如果出现后代选择器，为了防止该问题，可以在参数中显式地添加当前元素的选择器
