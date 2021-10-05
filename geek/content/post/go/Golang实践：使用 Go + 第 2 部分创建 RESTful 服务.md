
---
title: Golang实践：使用 Go + 第 2 部分创建 RESTful 服务
author: 知识铺
date: 2020-10-13 22:35:06+08:00
tags: [golang]
---
# <font _mstmutation="1" _msthash="29328" _msttexthash="34002657">什么是 RESTful 服务？</font>

<font _mstmutation="1" _msthash="34281" _msttexthash="1971112091">REST 是一种用于设计 Web 服务的体系结构方法。REST API 是围绕_资源_设计的，资源是客户端可以访问的任何类型的对象、数据或服务。资源具有标识符_，_它是唯一标识该资源的 URI。例如，特定客户订单的 URI 可能是：</font>

[https://adventure-works.com/orders/1](https://zshipu.com/t?url=https://adventure-works.com/orders/1)

<font _mstmutation="1" _msthash="29432" _msttexthash="1031287868">客户端通过交换资源表示形式_与服务_交互。许多 Web API 使用 JSON（当然不需要它）作为交换格式。例如，对上面列出的 URI 的 GET 请求可能会返回此响应正文：</font>

```{"orderId":1,"orderValue":99.90,"productId":1,"quantity":1}```

<font _mstmutation="1" _msthash="33826" _msttexthash="381965597">HTTP 协议定义了几种为请求分配语义意义的方法。大多数 RESTful Web API 使用的常见 HTTP 方法包括：</font>

*   <font _mstmutation="1" _msthash="22919" _msttexthash="345303088">**GET**在指定的 URI 中检索资源的表示形式。响应消息的正文包含请求资源的详细信息。</font>
*   <font _mstmutation="1" _msthash="29497" _msttexthash="704191813">**POST**在指定的 URI 上创建新资源。请求消息的正文提供新资源的详细信息。请注意，POST 还可用于触发实际不创建资源的操作。</font>
*   <font _mstmutation="1" _msthash="34021" _msttexthash="307301176">**PUT**在指定的 URI 上创建或替换资源。请求消息的正文指定要创建或更新的资源。</font>
*   <font _mstmutation="1" _msthash="35061" _msttexthash="241479823">**PATCH**执行资源的部分更新。请求正文指定要应用于资源的更改集。</font>
*   <font _mstmutation="1" _msthash="34190" _msttexthash="50225617">**删除**删除指定 URI 中的资源。</font>

<font _mstmutation="1" _msthash="38454" _msttexthash="1236853618">我们可以使用 GraphQL 或 gRPC 体系结构来构建我们的微服务结构。那我们为什么不呢？嗯， REST 相对易于实现。在未来的博客中，我将研究用上述一些技术重新设计后端。</font>

# <font _mstmutation="1" _msthash="34411" _msttexthash="29193541">文件结构如何？</font>

<font _mstmutation="1" _msthash="26988" _msttexthash="3474171961">在上一个博客中，我们添加了两个名为"你好"和"再见"的新处理程序。我们不再需要这些了， 所以我们删除了它们。相反，我们创建一个名为**产品的新处理程序**。我们将通过此处理程序执行 CRUD 操作。由于我们正在创建一个咖啡店，我们需要一个数据存储，存储我们的产品。**Product.go**将存储要存储的产品字段作为 go 结构。</font>



![image-20211005082401040](https://cdn.jsdelivr.net/gh/zshipu/images/202110050824634.png)



# <font _mstmutation="1" _msthash="32955" _msttexthash="41634892">产品处理程序和数据存储</font>

<font _mstmutation="1" _msthash="43979" _msttexthash="5716906039">让我们先看看我们的处理程序。我们首先检查 API 请求的 HTTP 谓词，即：GET、POST 和 PUT。我们还对产品结构**编写**方法。这些可以通过 p.MethodName 调用。这有助于抽象我们的逻辑和可再用性。如果您查看代码的基本结构，将看到一些函数编程的原则。**Golang**不是一**种**功能语言，但有很多功能**使我们能够在开发**中应用功能原则，使我们的代码更加优雅、简洁、可维护、更易于理解和测试。</font>

package handlersimport (
 "log"
 "net/http"
 "regexp"
 "strconv""github.com/nandangrover/go-microservices/data"
)//Products structure that holds a logger
type Products struct {
 l *log.Logger
}// NewProducts function return the pointer to Products structure
func NewProducts(l *log.Logger) *Products {
 return &Products{l}
}func (p *Products) ServeHTTP(rw http.ResponseWriter, r *http.Request) {
 if r.Method == http.MethodGet {
  p.getProducts(rw, r)
  return
 }
 if r.Method == http.MethodPost {
  p.addProduct(rw, r)
  return
 }
 if r.Method == http.MethodPut {
  // expect the id in the URI
  regex := regexp.MustCompile(`/([0-9]+)`)
  group := regex.FindAllStringSubmatch(r.URL.Path, -1)if len(group) != 1 || len(group[0]) != 2 {
   http.Error(rw, "Invalid URI", http.StatusBadRequest)
   return
  }idString := group[0][1]
  // Ignore the error for now
  id, _ := strconv.Atoi(idString)p.updateProducts(id, rw, r)
 }
 // catch all other http verb with 405
 rw.WriteHeader(http.StatusMethodNotAllowed)
}func (p *Products) getProducts(rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle GET products")listOfProducts := data.GetProducts()
 // Use encoder as it is marginally faster than json.marshal. It's important when we use multiple threads
 // d, err := json.Marshal(listOfProducts)
 err := listOfProducts.ToJSON(rw)
 if err != nil {
  http.Error(rw, "Unable to marshal json", http.StatusInternalServerError)
 }
}func (p *Products) addProduct(rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle POST product")prod := &data.Product{}
 // The reason why we use a buffer reader is so that we don't have to allocate all the memory instantly to a slice or something like that,
 err := prod.FromJSON(r.Body)
 if err != nil {
  http.Error(rw, "Unable to unmarshal json", http.StatusBadRequest)
 }
 // p.l.Printf("Prod %#v", prod)
 data.AddProduct(prod)
}func (p *Products) updateProducts(id int, rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle Put product")prod := &data.Product{}
 // The reason why we use a buffer reader is so that we don't have to allocate all the memory instantly to a slice or something like that,
 err := prod.FromJSON(r.Body)
 if err != nil {
  http.Error(rw, "Unable to unmarshal json", http.StatusBadRequest)
 }err = data.UpdateProduct(id, prod)
 if err == data.ErrProductNotFound {
  http.Error(rw, "Product not found", http.StatusNotFound)
  return
 }if err != nil {
  http.Error(rw, "Product not found", http.StatusInternalServerError)
  return
 }}

<font _mstmutation="1" _msthash="39832" _msttexthash="655781061">**我们**产品的数据存储定义了每个咖啡店产品的结构。我们需要导出产品，因此产品结构中的每个键都需要有一个大写第一字符。</font>

<font _mstmutation="1" _msthash="22386" _msttexthash="1494353250">我们还在此文件中存储一些帮助程序实用程序方法，如 ToJSON 和 FromJSON。这些方法有助于将我们的产品结构转换为 JSON，反之亦然。抽象在这里是绝对可能的，但我们将在下一个博客中多看一下。</font>

<font _mstmutation="1" _msthash="27612" _msttexthash="742656265">最后，我们还有我们的**可变产品列表**，它存储了对产品结构的引用的一部分。在切片中，我们添加了一些虚拟数据，可用于执行 CRUD 操作。</font>

package dataimport (
 "encoding/json"
 "fmt"
 "io"
 "time"
)//Product defines the structure for an API product
//Since encoding/json is a package residing outside our package we need to uppercase the first character of the fields inside the structure
//To get nice json field names we can add struct tags though. This will output the key name as the tag name
type Product struct {
 ID          int     `json:"id"`
 Name        string  `json:"name"`
 Description string  `json:"description"`
 Price       float32 `json:"price"`
 SKU         string  `json:"sku"`
 CreatedOn   string  `json:"-"`
 UpdatedOn   string  `json:"-"`
 DeletedOn   string  `json:"-"`
}// Products is a type defining slice of struct Product
type Products []*Product// ToJSON is a Method on type Products (slice of Product), used to covert structure to JSON
func (p *Products) ToJSON(w io.Writer) error {
 // NewEncoder requires an io.Reader. http.ResponseWriter is the same thing
 encoder := json.NewEncoder(w)
 return encoder.Encode(p)
}// FromJSON is a Method on type Products (slice of Product)
func (p *Product) FromJSON(r io.Reader) error {
 decoder := json.NewDecoder(r)
 return decoder.Decode(p)
}//GetProducts - Return the product list
func GetProducts() Products {
 return productList
}//AddProduct - Add the product to our struct Product
func AddProduct(p *Product) {
 p.ID = getNextID()
 productList = append(productList, p)
}//UpdateProduct - Updates the product to our struct Product
func UpdateProduct(id int, p *Product) error {
 _, pos, err := findProduct(id)
 if err != nil {
  return err
 }p.ID = id
 productList[pos] = preturn nil
}func findProduct(id int) (*Product, int, error) {
 for i, p := range productList {
  if p.ID == id {
   return p, i, nil
  }
 }
 return nil, -1, ErrProductNotFound
}// ErrProductNotFound is the Standard Product not found error structure
var ErrProductNotFound = fmt.Errorf("Product not found")// Increments the Product ID by one
func getNextID() int {
 lastProduct := productList[len(productList)-1]
 return lastProduct.ID + 1
}var productList = []*Product{
 &Product{
  ID:          1,
  Description: "Latte",
  Name:        "Milky coffee",
  SKU:         "abc323",
  Price:       200,
  UpdatedOn:   time.Now().UTC().String(),
  CreatedOn:   time.Now().UTC().String(),
 },
 &Product{
  ID:          2,
  Description: "Expresso",
  Name:        "Strong coffee",
  SKU:         "errfer",
  Price:       150,
  UpdatedOn:   time.Now().UTC().String(),
  CreatedOn:   time.Now().UTC().String(),
 },
}
# <font _mstmutation="1" _msthash="23777" _msttexthash="19841588">检索产品 + 获取</font>

<font _mstmutation="1" _msthash="28236" _msttexthash="295669699">要检索我们的产品，我们可以通过基于 Unix 的终端以这样的方式发送请求：</font>

curl -v localhost:9090 | jq

> <font _mstmutation="1" _msthash="29367" _msttexthash="32866067">jq 有助于格式化响应。</font>

<font _mstmutation="1" _msthash="23595" _msttexthash="890288425">产品.go 处理程序在此请求下激活。在 ServeHTTP 方法中，我们写了一个 if 条件，用于检查使用 http 请求的 HTTP 谓词。方法获取，本质上是字符串"GET"。</font>

if r.Method == http.MethodGet {
  p.getProducts(rw, r)
  return
 }

<font _mstmutation="1" _msthash="39416" _msttexthash="2325191349">**getproducts（）**方法是 GET 请求的。我们将 HTTP 响应编写器发送到此方法。此方法反过来从我们的数据存储**中获取**产品列表切片。由于它是一个切片，我们将其转换为 JSON，使用我们的 ToJSON 实用程序方法，该方法在结构产品的类型上定义。</font>

func (p *Products) getProducts(rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle GET products")listOfProducts := data.GetProducts()
 // Use encoder as it is marginally faster than json.marshal. It's important when we use multiple threads
 // d, err := json.Marshal(listOfProducts)
 err := listOfProducts.ToJSON(rw)
 if err != nil {
  http.Error(rw, "Unable to marshal json", http.StatusInternalServerError)
 }
}

<font _mstmutation="1" _msthash="28054" _msttexthash="9877518755">编码将 v 的 JSON 编码写入流，后跟一个新行字符。我们本可以用**json 的元帅**在这里，但我们没有。编码器和解码器将结构写入流切片或从流切片读取数据并将其转换为结构。在内部，它也实现封送方法。唯一的区别是，如果你想玩字符串或字节使用封送，如果任何数据，你想读取或写入一些编写器接口（如我们的响应编写器），使用编码和解码。这反过来也更快。我们不会注意到单个 API 调用有任何速度差异，但使用编码器而不是 Marshal 可以更好地处理数千个同时进行的 API 调用。您可以在此处阅读有关编码/json 包[的更多内容](https://zshipu.com/t?url=https://golang.org/pkg/encoding/json/#Encoder)。</font>

// ToJSON is a Method on type Products (slice of Product), used to covert structure to JSON
func (p *Products) ToJSON(w io.Writer) error {
 // NewEncoder requires an io.Reader. http.ResponseWriter is the same thing
 encoder := json.NewEncoder(w)
 return encoder.Encode(p)
}

<font _mstmutation="1" _msthash="35048" _msttexthash="280691177">因此，此编码器将我们的响应写入响应编写器。API 调用的最终输出有点像：</font>

[
  {
    "id": 1,
    "name": "Milky coffee",
    "description": "Latte",
    "price": 200,
    "sku": "abc323"
  },
  {
    "id": 2,
    "name": "Strong coffee",
    "description": "Expresso",
    "price": 150,
    "sku": "errfer"
  }
]
# <font _mstmutation="1" _msthash="33579" _msttexthash="13596141">添加新产品 + POST</font>

<font _mstmutation="1" _msthash="23517" _msttexthash="267359261">要添加新产品，我们可以通过基于 Unix 的终端以这样的方式发送请求：</font>

curl -v localhost:9090 -XPOST -d {"name": "Tea", "description": "Cuppa Tea", "price": 10}

<font _mstmutation="1" _msthash="23725" _msttexthash="806933088">添加产品的结构类似于获取产品。我们遵循相同的数据传输流程：到数据存储的处理程序。处理程序识别 HTTP 谓词并调用适当的方法，即**addProduct**。</font>

<font _mstmutation="1" _msthash="33644" _msttexthash="1430170313">此方法反过来创建对我们的产品结构的引用，该结构定义了我们的产品结构。请求正文中接收的 JSON 数据将发送到实用程序方法 FromJSON，以解码为我们定义的结构（即产品）的结构化引用。</font>

func (p *Products) addProduct(rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle POST product")prod := &data.Product{}
 // The reason why we use a buffer reader is so that we don't have to allocate all the memory instantly to a slice or something like that,
 err := prod.FromJSON(r.Body)
 if err != nil {
  http.Error(rw, "Unable to unmarshal json", http.StatusBadRequest)
 }
 // p.l.Printf("Prod %#v", prod)
 data.AddProduct(prod)
}

<font _mstmutation="1" _msthash="29705" _msttexthash="613383173">现在，我们已将产品存储为结构产品的参考，我们将它追加到**我们的产品列表切片中**，该切片用作我们的临时数据库存储。</font>

func AddProduct(p *Product) {
 p.ID = getNextID()
 productList = append(productList, p)
}

<font _mstmutation="1" _msthash="28886" _msttexthash="782232490">为我们的产品生成一个新的 ID，并附加到我们的切片。如果我们向我们的产品 API 发送 GET 请求，我们将看到现在列出的 3 种产品，而不是 2 个。</font>

[
  {
    "id": 1,
    "name": "Milky coffee",
    "description": "Latte",
    "price": 200,
    "sku": "abc323"
  },
  {
    "id": 2,
    "name": "Strong coffee",
    "description": "Expresso",
    "price": 150,
    "sku": "errfer"
  },{
    "id": 3,
    "name": "Tea",
    "description": "Cuppa Tea",
    "price": 10
  }
]
# <font _mstmutation="1" _msthash="28535" _msttexthash="18319717">更新现有产品 + PUT</font>

<font _mstmutation="1" _msthash="28093" _msttexthash="281818355">要更新现有产品，我们可以通过基于 Unix 的终端以这样的方式发送请求：</font>

curl -v localhost:9090/2 -XPUT -d {"name": "Frappuccino", "description": "Cuppa frappuccino", "price": 100}

<font _mstmutation="1" _msthash="31902" _msttexthash="891551752">更新产品的结构类似于获取产品。我们遵循相同的数据传输流程：到数据存储的处理程序。处理程序识别 HTTP 谓词并调用适当的方法，即**更新产品**。</font>

<font _mstmutation="1" _msthash="24024" _msttexthash="580421517">PUT 请求比简单的 POST 或 GET 更难解析，因为我们必须从 URI 中提取请求的 ID。我们如何做到这一点？我们使用一些 regexp 。</font>

<font _mstmutation="1" _msthash="27313" _msttexthash="3149617757">由于我们的 ID 是一个数字，我们编写一个 regexp 来搜索一组数字 （0+9），这些数字可以重复，由 + 标记表示。在运行 FindAllStringSubmatch 时，如果我们获得成功的匹配，匹配字符串将驻留在多维数组中。我们从索引 {0}{1} 中提取必要的组。我将留给您来找出为什么索引位于 {1} 而不是 {0}中。</font>

<font _mstmutation="1" _msthash="30017" _msttexthash="387511956">Regexp 真的很有趣， 在很多方面都很有帮助。您可以在此处阅读有关 Golang 标准库提供的方法[。](https://zshipu.com/t?url=https://golang.org/pkg/regexp/)</font>

if r.Method == http.MethodPut {
  // expect the id in the URI
  regex := regexp.MustCompile(`/([0-9]+)`)
  group := regex.FindAllStringSubmatch(r.URL.Path, -1)if len(group) != 1 || len(group[0]) != 2 {
   http.Error(rw, "Invalid URI", http.StatusBadRequest)
   return
  }idString := group[0][1]
  // Ignore the error for now
  id, _ := strconv.Atoi(idString)p.updateProducts(id, rw, r)
 }

<font _mstmutation="1" _msthash="34905" _msttexthash="283836826">现在，我们有我们需要更新的产品 ID，我们可以从请求正文中提取更新的信息。</font>

<font _mstmutation="1" _msthash="28730" _msttexthash="530932675">我们将从身体中解码为指向数据存储内产品的结构参考。此步骤类似于 POST 请求。接下来**将调用**数据存储中的 UpdateProduct 方法。</font>

func (p *Products) updateProducts(id int, rw http.ResponseWriter, r *http.Request) {
 p.l.Println("Handle Put product")prod := &data.Product{}
 // The reason why we use a buffer reader is so that we don't have to allocate all the memory instantly to a slice or something like that,
 err := prod.FromJSON(r.Body)
 if err != nil {
  http.Error(rw, "Unable to unmarshal json", http.StatusBadRequest)
 }err = data.UpdateProduct(id, prod)
 if err == data.ErrProductNotFound {
  http.Error(rw, "Product not found", http.StatusNotFound)
  return
 }if err != nil {
  http.Error(rw, "Product not found", http.StatusInternalServerError)
  return
 }}

<font _mstmutation="1" _msthash="29120" _msttexthash="4319252613">要更新我们的产品，我们需要先找到它。我们有 URI 的 ID 是件好事，因为这是我们产品的唯一唯一标识符。为此，我们通过遍听产品**列表切片**并返回产品参考、切片中的索引和错误（如果找到产品为零）。。我们使用此索引（pos 是此索引的变量名称），将引用替换为请求正文中收到的 JSON（显然它现在解码为对产品结构的引用）。</font>

//UpdateProduct - Updates the product to our struct Product
func UpdateProduct(id int, p *Product) error {
 _, pos, err := findProduct(id)
 if err != nil {
  return err
 }p.ID = id
 productList[pos] = preturn nil
}func findProduct(id int) (*Product, int, error) {
 for i, p := range productList {
  if p.ID == id {
   return p, i, nil
  }
 }
 return nil, -1, ErrProductNotFound
}

<font _mstmutation="1" _msthash="28821" _msttexthash="428141844">索引 2 中的产品现在应该已更新。如果我们向产品 API 发送 GET 请求，我们将看到第二个产品更新为新值。</font>

[
  {
    "id": 1,
    "name": "Milky coffee",
    "description": "Latte",
    "price": 200,
    "sku": "abc323"
  },
  {
    "id": 2,
    "name": "Frappuccino",
    "description": "Cuppa Frappuccino",
    "price": 100,
    "sku": "errfer"
  },{
    "id": 3,
    "name": "Tea",
    "description": "Cuppa Tea",
    "price": 10
  }
]

