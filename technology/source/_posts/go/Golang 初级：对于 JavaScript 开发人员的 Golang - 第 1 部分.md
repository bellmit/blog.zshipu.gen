
title: Golang 初级：对于 JavaScript 开发人员的 Golang - 第 1 部分
author: 知识铺
date: 2020-09-15 18:17:26
tags: go
---
 

如果您是 JavaScript 开发人员，考虑学习另一种编程语言，那么 Golang 是一个不错的选择。它很简单，有很多动量，非常有表现性，并且与JavaScript有一些相似之处。

**编辑**： 有人在评论中问我，为什么 JS 开发人员应该选择 Go 的所有可用选项。在我看来[，JS](https://zshipu.com/t?url=https://dev.to/deepu105/my-love-hate-relationship-with-javascript-3p66)不是一个完美的语言，因此学习很少的其他语言将大大有利于JS开发人员使用JS更务实，并将有助于巩固她/他的基本编程概念的知识更好。当然，有很多选择在那里像鲁斯特，去，哈克斯克尔，科特林等，但我认为去是一个伟大的地方开始，因为它最简单的所有可用的选项之一，并广泛采用。我的第二个选择是科特林或[鲁斯特](https://zshipu.com/t?url=https://dev.to/deepu105/my-first-impressions-of-rust-1a8o)。

这篇文章不是语言的比较或说，他们是非常相似的。它为 JavaScript 开发人员快速掌握 Golang 提供了指南。Go 的许多方面与 JavaScript 完全不同，我们也将触及这一点。

# [](#things-that-are-more-similar)<font _mstmutation="1" _msthash="290277" _msttexthash="20233720">更相似的东西</font>

在 Go 中有许多与 JavaScript 中的概念非常相似的东西。大多数不一样，但相似。让我们先把他们弄出去在本系列的第一部分中，我们将看到它们是如何相似的，并注意任何关键差异。

## [](#functions)<font _mstmutation="1" _msthash="303433" _msttexthash="5358925">功能</font>

JS 和 Go 中最类似的功能是函数。

### [](#similarities)<font _mstmutation="1" _msthash="304330" _msttexthash="10188503">相似 之 处</font>

*   功能是一流的公民。
*   函数可以分配给变量。
*   函数可以作为参数传递给其他函数，也可以从函数返回。
*   函数可以嵌套。
*   函数可以进行（部分函数）。
*   函数可以记住其周围上下文，从而创建闭包。
*   函数可以命名或匿名。可以立即调用匿名函数（IIFE）

**Javascript**

 <code>// A normal function with access to `this`
function standardFunction(arg1, arg2) {
    return `${arg1}:${arg2}`;
}

// A function assigned to a variable
const assignedFunction1 = standardFunction;

// An arrow function assigned to a variable
const assignedArrowFunction = (arg1, arg2) => {
    return `${arg1}:${arg2}`;
};

// A higher-order-function that accepts functions as argument and returns a function
function functionAsArgumentAndReturn(addFn, arg1, arg2) {
    const out = addFn(arg1, arg2);
    // This returns a closure
    return function(numArg) {
        return out + numArg;
    };
}

const out = functionAsArgumentAndReturn(
    (a, b) => {
        return a + b;
    },
    5,
    10
)(10);
// returns 25

// Nested functions
function nested() {
    console.log("outer fn");
    function nested2() {
        console.log("inner fn");
        const arrow = () => {
            console.log("inner arrow");
        };
        arrow();
    }
    nested2();
}

nested(); // prints:
// outer fn
// inner fn
// inner arrow

// this is a higher-order-function that returns a function
function add(x) {
    // A function is returned here as closure
    // variable x is obtained from the outer scope of this method and memorized in the closure
    return y => x + y;
}

// we are currying the add method to create more variations
var add10 = add(10);
var add20 = add(20);
var add30 = add(30);

console.log(add10(5)); // 15
console.log(add20(5)); // 25
console.log(add30(5)); // 35

// An anonymous function invoked immediately(IIFE)
(function() {
    console.log("anonymous fn");
})();
// prints: anonymous fn</code> 

**去**

 <code>// A normal function, this cannot be nested
func standardFunction(arg1 string, arg2 string) string {
    return fmt.Sprintf("%s:%s", arg1, arg2)
}

func main() {

    // A function assigned to a variable
    var assignedFunction1 = standardFunction

    // An anonymous function assigned to a variable and nested
    var assignedFunction2 = func(arg1 string, arg2 string) string {
        return fmt.Sprintf("%s:%s", arg1, arg2)
    }

    // A higher-order-function that accepts functions as argument and returns a function
    var functionAsArgumentAndReturn = func(addFn func(int, int) int, arg1 int, arg2 int) func(int) int {
        var out = addFn(arg1, arg2)
        // This returns a closure
        return func(numArg int) int {
            return out + numArg
        }
    }

    var out = functionAsArgumentAndReturn(
        func(a, b int) int {
            return a + b
        },
        5,
        10,
    )(10)
    fmt.Println(out) // prints 25

    // Nested anonymous functions
    var nested = func() {
        fmt.Println("outer fn")
        var nested2 = func() {
            fmt.Println("inner fn")
            var nested3 = func() {
                fmt.Println("inner arrow")
            }
            nested3()
        }
        nested2()
    }

    nested() // prints:
    // outer fn
    // inner fn
    // inner arrow

    // this is a higher-order-function that returns a function
    var add = func(x int) func(y int) int {
        // A function is returned here as closure
        // variable x is obtained from the outer scope of this method and memorized in the closure
        return func(y int) int {
            return x + y
        }
    }

    // we are currying the add method to create more variations
    var add10 = add(10)
    var add20 = add(20)
    var add30 = add(30)

    fmt.Println(add10(5)) // 15
    fmt.Println(add20(5)) // 25
    fmt.Println(add30(5)) // 35

    // An anonymous function invoked immediately(IIFE)
    (func() {
        fmt.Println("anonymous fn")
    })()
    // prints: anonymous fn

    assignedFunction1("a", "b")
    assignedFunction2("a", "b")
}</code> 

### [](#differences)<font _mstmutation="1" _msthash="306202" _msttexthash="4717674">差异</font>

*   <font _mstmutation="1" _msthash="464542" _msttexthash="1886259518">JavaScript 函数有两种形式;常规函数和箭头函数，而在 Go 中有正常函数和接口函数。普通 Go 函数没有 ，因此更类似于箭头函数，而接口函数具有类似于 a 的功能，因此更接近 JavaScript 中的正常函数。Go没有全球化的概念。</font>```this``````this``````this```

**Javascript**

 <code>function normalFnOutsideClass() {
    console.log(`I still can access global this: ${this}`);
}

const arrowFnOutsideClass = () => {
    console.log(`I don't have any this`);
};

class SomeClass {
    name = "Foo";
    normalFnInsideClass = function() {
        console.log(`I can access the callee as this: ${this.name}`);
    };
    arrowFnInsideClass = () => {
        console.log(`I can access the class reference as this: ${this.name}`);
    };
}

new SomeClass().normalFnInsideClass();
new SomeClass().arrowFnInsideClass();</code> 

**去**

 <code>type SomeStruct struct {
    name string
}

func (this *SomeStruct) normalFnInsideStruct() {
    // you can name the variable this or anything else
    fmt.Printf("I can access the struct reference as this\n: %s", this.name)
}

func main() {

    var normalFnOutsideStruct = func() {
        fmt.Println("I can access variables in my scope")
    }
    normalFnOutsideStruct()

    var structVal = SomeStruct{"Foo"}
    structVal.normalFnInsideStruct()
}</code> 

*   JavaScript 函数与任何其他值类型相同，因此甚至可以保留 Go 中不可能的其他属性。
*   Go 函数可以具有隐式命名返回。
*   只能在 Go 中嵌套匿名函数。
*   Go 函数可以返回多个值，而在 JavaScript 中只能返回一个值。但是，在 JS 中，您可以使用析构实现该方法，以便可以在两个函数中执行类似的查找函数

**Javascript**

 <code>function holdMyBeer() {
    return ["John", 2];
}

let [a, b] = holdMyBeer();
console.log(`Hey ${a}, hold my ${b} beer\n`);</code> 

**去**

 <code>func holdMyBeer() (string, int64) {
    return "John", 2
}

func main() {
    a, b := holdMyBeer()
    fmt.Printf("Hey %s, hold my %d beer\n", a, b)
}</code> 

## [](#scope)<font _mstmutation="1" _msthash="306540" _msttexthash="5367089">范围</font>

范围是变量有效的上下文，这决定了变量的可用用，并且 JS 和 Go 在这里有许多相似之处

### [](#similarities)<font _mstmutation="1" _msthash="304616" _msttexthash="10188503">相似 之 处</font>

*   两者都有函数范围和函数都可以记住其周围范围。
*   两者都有块范围。
*   两者都具有全局范围。

### [](#differences)<font _mstmutation="1" _msthash="305240" _msttexthash="4717674">差异</font>

*   <font _mstmutation="1" _msthash="463580" _msttexthash="304451225">Go 的概念在 JavaScript 中是一个棘手的概念。伊莫， 这使得事情在 Go 中简单得多。</font>```this```
*   <font _mstmutation="1" _msthash="463957" _msttexthash="201524297">无法在 Go 中重新声明同一作用域中的变量。Go 更接近 JS 中的关键字。</font>```var``````let```

## [](#flow-control)<font _mstmutation="1" _msthash="305591" _msttexthash="12147954">流量控制</font>

Golang 中的流控制在许多方面与 JavaScript 非常相似，但比 JavaScript 简单。

### [](#similarities)<font _mstmutation="1" _msthash="306488" _msttexthash="10188503">相似 之 处</font>

*   ```for```<font _mstmutation="1" _msthash="464828" _msttexthash="42140813">循环在两者中非常相似。</font>
*   ```while```<font _mstmutation="1" _msthash="465205" _msttexthash="96849454">循环非常相似，但 Go 使用相同的关键字。</font>```for```
*   ```forEach```<font _mstmutation="1" _msthash="465582" _msttexthash="87244378">在功能上也类似，但语法却大相径庭。</font>
*   您可以断开/继续循环。您也可以使用标签来这样做。
*   ```if/else```<font _mstmutation="1" _msthash="466336" _msttexthash="75230740">语法相当相似， Go 版本更强大一点</font>

**Javascript**

 <code>// For loop
for (let i = 0; i < 10; i++) {
    console.log(i);
}

// While loop
let i = 0;
while (i < 10) {
    console.log(i);
    i++;
}

// Do while

let j = 0;
do {
    j += 1;
    console.log(j);
} while (j < 5);

// ForEach loop
["John", "Sam", "Ram", "Sabi", "Deepu"].forEach((v, i) => {
    console.log(`${v} at index ${i}`);
});

// for of loop
for (let i of ["John", "Sam", "Ram", "Sabi", "Deepu"]) {
    console.log(i);
}

// For in loop
const obj = {
    a: "aVal",
    b: "bVal"
};

for (let i in obj) {
    console.log(obj[i]);
}</code> 

**去**

 <code>func main() {
    // For loop
    for i := 0; i < 10; i++ {
        fmt.Println(i)
    }

    // While loop
    i := 0
    for i < 10 {
        fmt.Println(i)
        i++
    }

    // Do while
    j := 0
    for {
        j += 1
        fmt.Println(j)
        if j == 5 {
            break
        }
    }

    // ForEach and for of loop
    for i, v := range []string{"John", "Sam", "Ram", "Sabi", "Deepu"} {
        fmt.Printf("%v at index %d\n", v, i)
    }

    // For in loop
    var obj = map[string]string{
        "a": "aVal",
        "b": "bVal",
    }

    for i, v := range obj {
        fmt.Printf("%v at index %s\n", v, i)
    }
}</code> 

### [](#differences)<font _mstmutation="1" _msthash="305539" _msttexthash="4717674">差异</font>

*   Go 中没有三元运算符。
*   ```switch```<font _mstmutation="1" _msthash="464256" _msttexthash="730070354">语句语法类似，但 Go 默认值要中断，JS 默认值将失败。在 Go 中，您可以在 JS 中使用该功能的关键字，而在 JS 中，我们有关键字。</font>```fallthrough``````break```
*   <font _mstmutation="1" _msthash="464633" _msttexthash="448257472">JS 有更多的迭代方法，如 、和 循环等，在 Go 中不可用，尽管大多数迭代方法都可以使用语法实现。</font>```while``````forEach``````for in``````for of``````for```
*   ```if/else```<font _mstmutation="1" _msthash="465010" _msttexthash="503965839">可以在 Go 中进行 init 分配。在下面的代码中，赋值的范围仅在 和 块内，不在 和 块之外。这在 JS 中是不可能的。</font>```val``````if``````else```

**去**

 <code>if val := getVal(); val < 10 {
    return val
} else {
    return val + 1
}</code> 

## [](#memory-management)<font _mstmutation="1" _msthash="306514" _msttexthash="11895208">内存管理</font>

内存管理也非常相似，除了 JS 和 Go 中的详细信息。

### [](#similarities)<font _mstmutation="1" _msthash="307411" _msttexthash="10188503">相似 之 处</font>

*   两者都是在运行时收集的垃圾。
*   两者都有堆和堆栈内存，这两者的意思相同。

### [](#differences)<font _mstmutation="1" _msthash="305214" _msttexthash="4717674">差异</font>

*   Go 的指针会向用户公开，而用户的内存管理则被抽象开，而在 JavaScript 指针中，指针完全抽象化，您只使用值和引用。
*   Go 使用并发三色标记和扫描算法，侧重于延迟，而 JS 引擎通常实现不同的算法，Mark-Sweep 是非常受欢迎的选择。例如，V8 引擎同时使用标记扫描算法和清除算法。

### [](#misc)<font _mstmutation="1" _msthash="305838" _msttexthash="6464926">杂项</font>

*   <font _mstmutation="1" _msthash="464179" _msttexthash="59013682">注释在两者中是相同的，与</font>```//``````/* */```
*   JS 和 Go 都支持导入其他模块，尽管行为不一样
*   <font _mstmutation="1" _msthash="464933" _msttexthash="59128147">设置超时在两者中都类似。 与。</font>```setTimeout(somefunction, 3*1000)``````time.AfterFunc(3*time.Second, somefunction)```
*   <font _mstmutation="1" _msthash="465309" _msttexthash="197953262">两者都有点差运算符与 。不过，Go 传播仅适用于接口数组/切片。</font>```console.log(...array)``````fmt.Println(array...)```
*   <font _mstmutation="1" _msthash="465686" _msttexthash="72473544">两者都有方法参数的 rest 运算符与 。</font>```...nums``````nums ...int```

# [](#conclusion)<font _mstmutation="1" _msthash="305916" _msttexthash="6674577">结论</font>

在这部分中，我们看到了两种语言中相似的概念。在系列的下一部分中，我们将看到 JS 和 Go 之间更不同的东西。下一部分中有更多的不同之处，但也请注意，有些差异相当微妙，因此对于 JavaScript 开发人员来说很容易消化。


