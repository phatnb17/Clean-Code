# Summary

1. Introduction
2. Naming rule
3. Function
4. Comments
5. Error Handling

# 1. Introduction

Problems:

- Bạn có thể hiểu mã của mình hoặc đồng nghiệp trong bao lâu sau vài tháng?

 - Đã bao nhiêu lần bạn nói "Chúng ta có thể làm lại được không?"

 - Đã bao nhiêu lần bạn nói "Tài liệu mã ở đâu hoặc Bình luận ở đâu"?

 - Đã bao nhiêu lần bạn nhầm lẫn giữa mã và tài liệu bình luận hiện tại?

 - Đã bao nhiêu lần bạn nói với quản lý của mình rằng tôi không biết mọi việc đang diễn ra như thế nào. Nó rất kì lạ ?

 - Sửa chữa hoặc thay đổi một cái gì đó và tạo ra nhiều lỗi

 - ...
 - Bạn đang vội phải không?

 - Bạn có cố gắng đi "nhanh" không?

 - Bạn không có thời gian để làm tốt công việc?

 - Bạn có cảm thấy mệt mỏi khi làm việc cùng một chương trình/mô-đun
 không?

 - Sếp của bạn có ép bạn phải hoàn thành sớm không?

 Nếu bạn nói "Tôi sẽ quay lại sửa nó sau" bạn có thể rơi vào định
 luật LeBlanc: Later equals never (Để sau có nghĩa là không bao giờ).

 Sẽ là thiếu chuyên nghiệp nếu các lập trình viên tuân theo ý muốn của
 những người quản lý không hiểu được những rủi ro khi gây

 ra tình trạng lộn xộn.

 Có thể đôi khi bạn nghĩ phải đi thật nhanh để kịp thời hạn. Cách duy
 nhất để đi nhanh là giữ mã luôn sạch nhất có thể.

 Làm thế nào chúng ta có thể làm cho mã sạch?

## 2. Naming rule

### Meaningful names

Names are everywhere in software. Files, directories, variables functions, etc. Because we do so much of it. We have better do it well.

### Use Intention-Revealing Names (Nói trực tiếp ngữ cảnh)

 Việc chọn tên hay cần có thời gian nhưng lại tiết kiệm được nhiều hơn.
 Vì vậy, hãy cẩn thận với tên của bạn và thay đổi chúng khi bạn tìm thấy những cái tên tốt hơn.

 Tên của một biến, hàm hoặc lớp sẽ trả lời tất cả các câu hỏi lớn.

 Nó sẽ cho bạn biết lý do tại sao nó tồn tại, nó làm gì và được sử dụng
 như thế nào.

 Nếu một cái tên cần được bình luận thì cái tên đó không bộc lộ ý định
 của nó.

| Does not reveals intention       | Reveals intention       |
| -------------------------------- | ----------------------- |
| `var d; // elapsed time in days` | `var elapsedTimeInDays` |

**Bad:**

```
// Get male teenagers
const filterUsers = users.filter(u = (u.age = AGE.9 && u.age <= AGE.18) && u.gender === GENDER.MALE);

...

// What is filterUsers ?, you have to go the definition of filterUsers to see
vaccinated(filterUsers);

```

**Good:**

```
const isMaleTeenagers = (user) = (user.age = AGE.9 && user.age <= AGE.18)
                                        && user.gender === GENDER.MALE;
...

const maleTeenagers = users.filter(u = isTeenagers(age));

...

vaccinated(maleTeenagers);

```

###  Tránh thông tin sai lệch

- Người lập trình phải tránh để lại những manh mối sai làm che khuất ý nghĩa của mã. Chúng ta nên tránh những từ có ý nghĩa cố định khác với ý nghĩa dự định của chúng tôi.
```
const listProduct = await getProducts(); // OK we think it will return the list

...

const listProduct = await getProducts();  // return [ {categoryName: "Fish", products: [... ] }];
```

nên là

```
const groupOfCategoryProducts = await getProducts();
```

- Cẩn thận với việc sử dụng những tên khác nhau một chút

```
class ShoppingCartServiceForCaching {}

class ShoppingCartServiceForUserDefault{}

class ShoppingCartServiceForNetWorkCalls {}

```

Bạn có thể chọn sai tên khi ide gợi ý cho bạn lớp danh sách

nên là

```
class CacheService {}

class UserDefaultService {}

class NetworkClient {}
```

Không cần quét toàn bộ tên khi gõ

### Tạo sự khác biệt có ý nghĩa

Trình viên tự tạo ra vấn đề cho chính mình khi họ viết mã chỉ để đáp ứng trình biên dịch hoặc trình thông dịch. 
Ví dụ: vì bạn không thể sử dụng cùng một tên để chỉ hai thứ khác nhau
 trong cùng một phạm vi, nên bạn có thể muốn thay đổi một tên theo cách tùy ý.
```
function copyItems(a1, a2) {
    for (let i = 0; i < a1.length; i++) {
        a2[i] = a1[i];
    }
}
```

nên là

```
function copyItems(source, destination) {
    for (let i = 0; i < source.length; i++) {
        destination[i] = source[i];
    }
}
```

Những từ ồn ào là vô nghĩa.

```
const userInfo = getUserInfo();
const userData = getUserData();

```

Những từ ồn ào là dư thừa

```
const nameString = '';
const streetString = '';
const currentIdNumber = '1';
```

### Sử dụng tên có thể phát âm được

```
class DtaRcrd102 {
}
```

nên là

```
class Customer {
}
```

### Sử dụng tên có thể tìm kiếm

Tên gồm một chữ cái và hằng số có một vấn đề đặc biệt là chúng không dễ xác định vị trí trên toàn bộ văn bản.

### Class Names

Các lớp và đối tượng phải có tên 'danh từ' hoặc 'cụm danh từ' như Khách hàng, WikiPage, Tài khoản và Trình phân tích địa chỉ. Tên lớp không nên là một động từ.

### Tên phương thức

Các phương thức nên có tên động từ hoặc cụm động từ như postPayment, deletePage hoặc save

### Don't Be Cute

| Cute name         | Clean name    |
| ----------------- | ------------- |
| `holyHandGranade` | `deleteItems` |
| `whack`           | `kill`        |
| `eatMyShorts`     | `abort`       |

### Chọn một từ cho mỗi khái niệm

Chọn một từ cho một khái niệm trừu tượng và gắn bó với nó. Ví dụ, thật khó hiểu khi có các phương thức tìm nạp, truy xuất và nhận tương đương của các lớp khác nhau.

## 3. Functions

### Small!

Nguyên tắc đầu tiên của hàm là chúng phải nhỏ. Nguyên tắc thứ hai của hàm là chúng phải nhỏ hơn thế.

### Do One Thing

FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.

**Bad:**
```
class LinkedInProfile {
    
    getProfile() {
        this.view += 1;
        this.updatedAt = Date.now.toString();
        return this.information;
    }
}
```
**Good:**
```
class LinkedInProfile {
    
    getProfile() {
        return this.information;
    }

    increaseView() {
        this.view += 1;
        this.updatedAt = Date.now.toString();
    }
}
```

###  Một mức độ trừu tượng cho mỗi hàm

Để đảm bảo các hàm của chúng ta đang thực hiện "một việc", chúng ta cần đảm bảo rằng các câu lệnh trong hàm của chúng ta đều ở cùng một mức độ trừu tượng.

Đọc mã từ trên xuống dưới: _Quy tắc bước xuống_

Chúng tôi muốn mã đọc giống như một câu chuyện từ trên xuống. 5 Chúng tôi muốn mọi chức năng được theo sau bởi các chức năng ở mức độ trừu tượng tiếp theo để chúng tôi có thể đọc chương trình, giảm dần một mức độ trừu tượng tại một thời điểm khi chúng tôi đọc danh sách các chức năng.

Nói cách khác, chúng ta muốn có thể đọc chương trình như thể nó là một tập hợp của các đoạn TO, mỗi đoạn mô tả mức độ trừu tượng hiện tại và tham chiếu các đoạn TO tiếp theo ở cấp độ tiếp theo.

```
- Để bao gồm các phần thiết lập và phân tích, chúng tôi bao gồm các
 thiết lập, sau đó chúng tôi bao gồm nội dung trang thử nghiệm và sau
 đó chúng tôi bao gồm các phần phân tích.

 - Để bao gồm các thiết lập, chúng tôi bao gồm thiết lập bộ nếu đây là
 một bộ, sau đó chúng tôi bao gồm thiết lập thông thường.

 - Để bao gồm thiết lập bộ phần mềm, chúng tôi tìm kiếm phân cấp chính
 cho trang "SuiteSetUp" và thêm câu lệnh include kèm theo đường dẫn của
 trang đó.

 - Để tìm kiếm cha mẹ...
```

 Hóa ra là rất khó để các lập trình viên học cách tuân theo quy tắc này
 và viết các hàm duy trì ở một mức độ trừu tượng duy nhất. Nhưng học
 thủ thuật này cũng rất quan trọng. Đó là chìa khóa để giữ các chức
 năng ngắn gọn và đảm bảo chúng thực hiện "một việc". Làm cho mã được
 đọc giống như một tập hợp các đoạn TO từ trên xuống là một kỹ thuật
 hiệu quả để giữ mức độ trừu tượng nhất quán.

```
async function createOrder(request) {

    // Validation
    const { products, shippingAddress } = request;
    if (!products) {
        throw new ValidationError('Missing products');
    }
    ... validate many properties in request
    ....

    // Check existed products
    const productIds = products.map(p = p.id);
    const existedProductsResult = await productRepository.findMany(productIds);
    if (existedProductsResult.isFailure) {
        throw new BadRequestError();
    }
    const isProductsHaveNotTheSameSize = products.length !== existedProducts.length;
    if (isProductsHaveNotTheSameSize) {
        throw new BadRequestError('Some products are not existed');
    }

    // Checking price of products
    const existedProducts = existedProductsResult.value;
    for (const product of products) {
        const foundProduct = existedProducts.find(p = p.id === product.id);
        if (foundProduct.price !== product.price) {
            throw new BadRequestError('Wrong Price');
        }
    }

    // Save to DB
    const order = Order.create(request);
    const response = await orderRepository.save(order);

    return {
        message: 'Create order successfully,
    }
}
```

nên là

```
async function getProducts(products) {
    const productIds = products.map(p = p.id);
    const existedProductsResult = await productRepository.findMany(productIds);
    if (existedProductsResult.isFailure) {
        return Result.fail(existedProductsResult.error);
    }

    const isProductsHaveNotTheSameSize = products.length !== existedProducts.length;
    if (isProductsHaveNotTheSameSize) {
        return Result.fail(isProductsHaveNotTheSameSize);
    }
}

function isProductsHasCorrectPrice(sourceProducts, destinationProducts) {
    for (const product of sourceProducts) {
        const foundProduct = destinationProducts.find(p = p.id === product.id);
        if (foundProduct.price !== product.price) {
            return false;
        }
    }
    return true;
} 

async function createOrder(request) {

    const validatorResult = SchemaValidator.validate(request);
    if (validatorResult.isFailure) {
        throw new BadRequest(validatorResult.message);
    }
   
    const existedProductsResult = await this.getProducts(products);
    if (existedProductResult.isFailure) {
        throw new BadRequestError(existedProductResult.error);
    }

    if (!this.isProductsHasCorrectPrice(products, existedProductsResult.value)) {
        throw new BadRequestError('Wrong Price');
    }

    const order = Order.create(request);
    const response = await orderRepository.save(order);
    return {
        message: 'Create order successfully,
    }
}
```
###  Chuyển đổi câu lệnh
Thật khó để đưa ra một tuyên bố chuyển đổi nhỏ. 6 Ngay cả một câu lệnh
 chuyển đổi chỉ có hai trường hợp cũng lớn hơn

 mức tôi muốn có một khối hoặc hàm duy nhất. Thật khó để đưa ra một
 tuyên bố chuyển đổi thực hiện một việc. Về bản chất,

 các câu lệnh switch luôn làm N việc. Thật không may, chúng ta không
 phải lúc nào cũng tránh được các câu lệnh

 switch, nhưng chúng ta có thể đảm bảo rằng mỗi câu lệnh switch được
 chôn trong một lớp cấp thấp và không bao giờ được

 lặp lại. Tất nhiên, chúng tôi làm điều này với tính đa hình.

```
class EventManager {

    constructor({
        ..// Injections
    })
    async processEvent(message)  {
        switch(message.typeId) {
            case 1:
                justSave(message);
                break;
            case 2:
                notifyAll(message);
                break;
            case 3:
                notify(message);
                break;
            ...
        }
    }
}
```

nên là

```
class Message {
    processMessage(message) {};
}

class StorableMessage extends Message { 

    // Override
    processMessage(message) {
        justSave(message);
    }
}

class PublicMessage extends Message {

    // Override
    processMessage(message) {
        notifyAll(message);
    }
}

class PrivateMessage extends Message { 

    // Override
    processMessage(message) {
        notify(message);
    }
}

class MessageHandlerService {
    
    constructor() {
        this.mapHandler = new Map();

        this.mapHandler.set(1, new StorableMessage());
        this.mapHandler.set(2, new PublicMessage());
        this.mapHandler.set(3, new PrivateMessage());
    }

    async processMessage(message) {
        if (!this.mapHandler.has(message.type)) 
            throw new TypeError('This type is not existed');
        const handler = this.mapHandler.get(message.type);
        await handler.processMessage(message);
    }
}

const messageHandlerService = new MessageHandlerService();
const processEvent = (message) = {
    messageHandlerService.processMessage(message);
}

// Or using Factory
class MessageHandlerFactory {
    
    static getHandler(message) {
        switch(message.type) {
            case 1: return new StorableMessage();
            case 2: return new PublicMessage();
            case 3: return new PrivateMessage();
        }
    }
}

const processEvent = (message) = {
    const handler = MessageHandlerFactory.getHandler(message);
    handler.processMessage(message);
}
```
### Sử dụng tên mô tả

 Bạn biết rằng bạn đang làm việc với mã sạch khi mỗi quy trình đều đạt
 được gần như những gì bạn mong đợi

 Một nửa cuộc chiến để đạt được nguyên tắc đó là chọn những cái tên hay
 cho các chức năng nhỏ làm một việc.

 Chức năng càng nhỏ và tập trung thì càng dễ chọn tên mô tả.

 Đừng ngại đặt tên dài. Một cái tên mang tính mô tả dài sẽ tốt hơn một
 cái tên ngắn gọn, bí ẩn. Một tên mô tả

 dài sẽ tốt hơn một nhận xét mô tả dài. Sử dụng quy ước đặt tên cho
 phép dễ dàng đọc nhiều từ trong tên hàm,

 sau đó tận dụng nhiều từ đó để đặt tên cho hàm cho biết chức năng của
 nó.

 Việc chọn tên mô tả sẽ làm rõ thiết kế của mô-đun trong đầu bạn và
 giúp bạn cải thiện nó. Không có gì lạ khi

 việc săn lùng một cái tên hay sẽ dẫn đến việc tái cấu trúc mã một cách
 thuận lợi.

### Đối số hàm

Việc giới hạn số lượng tham số hàm là vô cùng quan trọng vì nó giúp việc kiểm tra hàm của bạn dễ dàng hơn. Có nhiều hơn ba sẽ dẫn đến sự bùng nổ tổ hợp trong đó bạn phải kiểm tra hàng tấn trường hợp khác nhau với mỗi đối số riêng biệt.

 Một hoặc hai đối số là trường hợp lý tưởng và nên tránh ba đối số nếu
 có thể. Bất cứ điều gì nhiều hơn thế nên được củng cố. Thông thường, nếu bạn có nhiều hơn hai đối số thì hàm của bạn đang cố gắng thực hiện quá nhiều. Trong trường hợp không phải như vậy, hầu hết trường hợp, một đối tượng cấp cao hơn sẽ đủ làm đối số.

 Vì JavaScript cho phép bạn tạo các đối tượng một cách nhanh chóng mà
 không cần nhiều bản soạn sẵn lớp, nên bạn có thể sử dụng một đối tượng nếu thấy mình cần nhiều đối số.

 Để làm rõ những thuộc tính mà hàm mong đợi, bạn có thể sử dụng cú pháp cấu trúc ES2015/ES6. Điều này có một số lợi thế:

 Khi ai đó nhìn vào chữ ký hàm, sẽ ngay lập tức biết rõ thuộc tính nào đang được sử dụng. Nó có thể được sử dụng để mô phỏng các tham số được đặt tên. Việc hủy cấu trúc cũng sao chép các giá trị nguyên thủy được chỉ định của đối tượng đối số được truyền vào hàm. Điều này có thể giúp ngăn ngừa tác dụng phụ. Lưu ý: các đối tượng và mảng bị hủy cấu trúc khỏi đối số đối tượng KHÔNG được nhân bản. Linters có thể cảnh báo bạn về các thuộc tính không được sử dụng, điều này là không thể nếu không phá hủy.


```
function createMenu(title, body, buttonText, cancellable) {
  // ...
}

createMenu("Foo", "Bar", "Baz", true);

// Other way
function createMenu(menu) {
  // ...
}
```

nên là 
```
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true
});

```

### Không sử dụng cờ làm tham số hàm. Cờ cho người dùng biết rằng hàm này thực hiện nhiều chức năng. Chức năng nên làm một việc. Tách các hàm của bạn ra nếu chúng đi theo các đường dẫn mã khác nhau dựa trên boolean.

```
class Dog {
    run(isRun) {
        this.isRun = isRun
    }
}

const dog = new Dog();
dog.run(true);
dog.run(false);

```
nên là 

```
class Dog {
    run() {
        this.isRun = true;
        ...
    }

    stop () {
        this.isRun = false;
        ...
    }
}
```
### Phản ứng phụ
Trong JavaScript, một số giá trị không thể thay đổi (không thay đổi)
 và một số giá trị có thể thay đổi (có thể thay đổi). Đối tượng và mảng
 là hai loại giá trị có thể thay đổi nên điều quan trọng là phải xử lý
 chúng cẩn thận khi chúng được truyền dưới dạng tham số cho hàm. Hàm
 JavaScript có thể thay đổi thuộc tính của đối tượng hoặc thay đổi nội
 dung của một mảng, điều này có thể dễ dàng gây ra lỗi ở nơi khác.

Giả sử có một hàm chấp nhận tham số mảng đại diện cho giỏ hàng. Nếu
 hàm thực hiện thay đổi trong mảng giỏ hàng đó - ví dụ: bằng cách thêm
 một mặt hàng để mua - thì bất kỳ hàm nào khác sử dụng cùng mảng giỏ
 hàng đó sẽ bị ảnh hưởng bởi sự bổ sung này. Điều đó có thể là tuyệt
 vời, tuy nhiên nó cũng có thể là điều tồi tệ. Hãy tưởng tượng một tình
 huống xấu:

 Người dùng nhấp vào nút "Mua hàng" để gọi chức năng mua hàng nhằm
 tạo ra yêu cầu mạng và gửi mảng giỏ hàng đến máy chủ. Do kết nối mạng
 kém nên chức năng mua hàng phải tiếp tục thử lại yêu cầu. Bây giờ,
 điều gì sẽ xảy ra nếu trong lúc chờ đợi, người dùng vô tình nhấp vào
 nút "Thêm vào giỏ hàng" trên một mặt hàng mà họ thực sự không muốn
 trước khi yêu cầu mạng bắt đầu? Nếu điều đó xảy ra và yêu cầu mạng bắt
 đầu thì chức năng mua hàng đó sẽ gửi mặt hàng vô tình được thêm vào do
 mảng giỏ hàng đã được sửa đổi.

Một giải pháp tuyệt vời là hàm addItemToCart luôn sao chép giỏ hàng,
 chỉnh sửa và trả lại bản sao. Điều này sẽ đảm bảo rằng các chức năng
 vẫn đang sử dụng giỏ hàng cũ sẽ không bị ảnh hưởng bởi những thay đổi.

Hai lưu ý cần đề cập đến cách tiếp cận này:

 Có thể có những trường hợp bạn thực sự muốn sửa đổi đối tượng đầu vào,
 nhưng khi áp dụng phương pháp lập trình này, bạn sẽ thấy rằng những
 trường hợp đó khá hiếm. Hầu hết mọi thứ có thể được tái cấu trúc để
 không có tác dụng phụ!

Nhân bản các đối tượng lớn có thể rất tốn kém về mặt hiệu suất. May
 mắn thay, đây không phải là vấn đề lớn trong thực tế vì có những thư
 viện tuyệt vời cho phép phương pháp lập trình này nhanh chóng và không
 tốn nhiều bộ nhớ như khi bạn sao chép thủ công các objects và arrays.e

```
// Before login
let tokenPayload = null;

// After login
tokenPayload = {
    id: '12321',
    username: 'Thang Cao',
    role: 'admin'
}

// Some process
function someProcess () {
    const token = tokenPayload;

    doSomething1(token);
    doSomething2(token);
}

function doSomething1(token) {
    console.log('Token: ', token);
}

function doSomething2(token) {
    token.username = 'GT';
}

someProcess();
console.log('Token: ', tokenPayload);
```

### Đừng lặp lại chính mình

Sự sao chép có thể là gốc rễ của mọi tội lỗi trong phần mềm. Nhiều
 nguyên tắc và thực tiễn đã được tạo ra nhằm mục đích kiểm soát hoặc
 loại bỏ nó.

## 4. Bình luận
Không có gì có thể hữu ích bằng một bình luận được đặt đúng chỗ. Không
 có gì có thể làm lộn xộn một mô-đun hơn những nhận xét giáo điều phù
 phiếm. Không gì có thể gây tai hại bằng một bình luận cũ tuyên truyền
 dối trá và thông tin sai lệch.


 Nếu ngôn ngữ lập trình của chúng tôi đủ biểu cảm hoặc nếu chúng tôi có
 tài năng sử dụng những ngôn ngữ đó một cách tinh tế để thể hiện ý định
 của mình, thì chúng tôi sẽ không cần nhận xét nhiều---có lẽ là không
 hề.
### Nhận xét không bù đắp cho mã xấu

 Mã rõ ràng và biểu cảm với ít bình luận sẽ vượt trội hơn nhiều so với
 mã lộn xộn và phức tạp với nhiều bình luận. Thay vì dành thời gian
 viết bình luận để giải thích mớ hỗn độn mà bạn đã gây ra, hãy dành
 thời gian để dọn dẹp mớ hỗn độn đó.


### Giải thích bản thân bằng mã
**Bad:**
```
// Check user is male teenager
if (user.age = AGE.9 && user.age <= AGE.18) && user.gender === GENDER.MALE)
```

**Good:**
```
if (isMaleTeenager(user))
```

### TODO Comments
Đôi khi, việc để lại ghi chú "Việc cần làm" ở dạng // nhận xét TODO là
 hợp lý. Trong trường hợp sau, nhận xét TODO giải thích lý do tại sao
 hàm này có cách triển khai suy biến và tương lai của hàm đó sẽ như thế
 nào.
```
// TODO: hỗ trợ phân trang và thêm một số thông số truy vấn
function fetchUsers() {}
```
TODO là những công việc mà người lập trình nghĩ nên làm nhưng vì lý do
 nào đó lại không thể làm được vào lúc này. Đó có thể là lời nhắc xóa
 một tính năng không được dùng nữa hoặc lời cầu xin người khác xem xét
 vấn đề. Đó có thể là yêu cầu người khác nghĩ ra một cái tên hay hơn
 hoặc một lời nhắc nhở thực hiện thay đổi tùy thuộc vào một sự kiện đã
 được lên kế hoạch. Dù TODO có thể là gì đi nữa thì đó không phải là lý
 do để để lại mã xấu trong hệ thống.

### Bad Comments

#### Bình luận dư thừa

Một nhận xét là dư thừa nếu nó mô tả điều gì đó mô tả chính nó một cách đầy đủ.
For example

```
i++; // increment

const apiOptions = {
    url: '', // Host Url 
    port: '' // Port number
}

class ShoppingCart {

    // This function will return total price of shopping cart
    getTotalPrice() {

    }
}
```

### Noise Comments
```
// The day of the month
const dayOfMonth;
```

### Too Much Information
những cuộc thảo luận lịch sử thú vị hoặc những mô tả chi tiết không liên quan vào nhận xét của bạn.

###  Đừng để lại mã đã nhận xét trong cơ sở mã của bạn Kiểm soát phiên bản tồn tại là có lý do. Để lại mã cũ trong lịch sử của bạn.
**Bad:**
```
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```
**Good:**
```
doStuff()
```

## 5. Xử lý lỗi

### Đừng bỏ qua các lỗi đã phát hiện

**Bad:**
```
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
```
**Good:**

```
try {
  functionThatMightThrow();
} catch (error) {
  // One option (more noisy than console.log):
  console.error(error);
  // Another option:
  notifyUserOfError(error);
  // Another option:
  reportErrorToService(error);
  // OR do all three!

  throw error;
}
```

### Đừng trả về giá trị rỗng
Nếu bạn muốn trả về null từ một phương thức, thay vào đó hãy xem xét
 việc ném một ngoại lệ hoặc trả về một đối tượng TRƯỜNG

 HỢP ĐẶC BIỆT. Nếu bạn đang gọi một phương thức trả về null từ API của
 bên thứ ba, hãy xem xét gói phương thức đó bằng một

 phương thức đưa ra một ngoại lệ hoặc trả về một đối tượng trường hợp
 đặc biệt.

### Đừng vượt qua giá trị rỗng

Trả về null từ các phương thức là xấu, nhưng chuyển null vào các
 phương thức còn tệ hơn. Trừ khi bạn đang làm việc với một

 API yêu cầu bạn chuyển giá trị rỗng, bạn nên tránh chuyển giá trị rỗng
 vào mã của mình bất cứ khi nào có thể.


