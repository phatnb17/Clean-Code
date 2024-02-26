# Summary

1. Introduction
2. Naming rule
3. Function
4. Comments

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
 những người quản lý không hiểu được những rủi ro khi gây ra tình trạng lộn xộn.

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

- Người lập trình phải tránh để lại những manh mối sai làm che khuất ý nghĩa của mã. Chúng ta nên tránh những từ có ý nghĩa cố định khác với ý nghĩa dự định của chúng ta.
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

Lập trình viên tự tạo ra vấn đề cho chính mình khi họ viết mã chỉ để đáp ứng trình biên dịch hoặc trình thông dịch. 
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

Các lớp và đối tượng phải có tên 'danh từ' hoặc 'cụm danh từ' như Customer, WikiPage, Account, and AddressParser. Tên lớp không nên là một động từ.

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

### Sử dụng tên mô tả

```
You know you are working on clean code when each routine turns out to be pretty much what you expected
```

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

