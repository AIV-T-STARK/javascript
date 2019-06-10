# Javascript

## Sự khác nhau giữa let và var

- var cho phép khai báo lại biến, còn let thì không.
-	var thì có tính chất hoisting, let thì không.
-	let chỉ tồn tại trong block scope, biến sẽ chết khi ra ngoài scope.

## Object
1. Cách 1: Object literal

```
// Khai báo toàn bộ các trường và hàm
var person = {
  firstName: 'Gia Hao',
  lastName: 'Nguyen',
  showName: function() {
    console.log(this.firstName + ' ' + this.lastName);
  }
};

```

- Class đâu? Không có class thì sao có Object?

2. Cách 2 : Object constructor

```
var psn = new Object();
psn.firstName = 'Gia Hao';
psn.lastName = 'Nguyen';
psn.showName = function() {
    console.log(this.firstName + ' ' + this.lastName);
  };
```

- Ta có thể hiểu toàn bộ object đều có class chung là Object

3. Cách 3 :
- 1 function sẽ đóng vai trò constructor để khởi tạo Object.
```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.showName = function() {
     console.log(this.firstName + ' ' + this.lastName);
  };
}

// Khi muốn tạo object person chỉ cần gọi constructor
var psn1 = new Person('Gia Hao', 'Nguyen');
var psn2 = new Person('VNP', 'Group');
```

## Con trỏ "this"
- Nếu this được sử dụng bên trong một hàm (tạm gọi là hàm A) thì nó sẽ chứa giá trị của đối tượng gọi hàm A. Chúng ta cần this để truy cập đến các phương thức và thuộc tính của đối tượng gọi hàm A, bởi vì chúng ta thường không biết tên của đối tượng đó. Thậm chí có lúc không có tên nào có thể dùng để tham chiếu đến đối tượng, chúng ta chỉ có thể dùng this mà thôi. Thực tế, this có thể coi là một tham chiếu đến "đối tượng tiền đề" - đối tượng gọi hàm.

```
var person = {
  firstName: 'Gia Hao',
  lastName: 'Nguyen',
  showName: function() {
    // this ở đây là person
    console.log(this.lastName + ' ' + this.firstName);
  }
};
person.showName(); // Nguyen Gia Hao
```

```
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.showName = function() {
     console.log(this.lastName + ' ' + this.firstName);
  };
}

var psn1 = new Person('Gia Hao', 'Nguyen');
psn1.showName(); //Nguyen Gia Hao
//this ở đây là psn1

var psn2 = new Person('Group', 'VNP');//VNP Group
psn2.showName(); //VNP Group
//this ở đây là psn2
```

### Lưu ý: 
- ‘this’ trong việc sử dụng hàm callback

```
var user = {
    data: [
        {name: "T. Woods", age: 37},
        {name: "P. Mickelson", age: 43}
    ],
    clickHandler:function(event) {
        // Chọn ngẫu nhiên 0 hoặc 1
        var randomNum = ((Math.random() * 2 | 0) + 1) - 1;

        // Dòng dưới đây sẽ in ra tên và tuối của một user ngẫu nhiên lấy từ array
        console.log(this.data[randomNum].name + " " + this.data[randomNum].age);
    }
}

var btn = document.querySelect(".btn");
btn.addEventListener("click", user.clickHandler); //undefined vì this ở đây tham chiếu đến đối tượng btn
```

để giải quyêt chúng ta sử dụng `bind`:
```
btn.addEventListener("click", user.clickHandler.bind(user));
```

- Sử dụng 'this' trong một hàm lồng trong hàm khác
```
var user = {
    hi: "Hi",
    data: [
        {name: "T. Woods", age: 37},
        {name: "P. Mickelson", age: 43}
    ],

    clickHandler: function() {
        // Việc sử dụng this.data ở đây không vấn đề gì, bởi vì "this"
        // tham chiếu đến đối tượng user và data là một thuộc tính của
        // đối tượng.
        this.data.forEach(function(person) {
            // Nhưng ở trong hàm vô danh này (nó được truyền cho
            // phương thức forEach), "this" không tham chiếu đến đối
            // tượng user nữa.  Hàm này không thể truy cập "this" của
            // hàm bên ngoài.
            console.log("What is your name?");
            console.log(this.hi + ".My name is " + person.name); // this ở đây được JS hiểu là [object Window]
        })
    }
}
```
giải pháp: 
```
clickHandler: function() {
  var theUserObj = this;
  this.data.forEach(function(person) {
      console.log("What is your name?");
      console.log(theUserObj.hi + ".My name is " + person.name);
  })
}
```

- Sử dụng this khi phương thức được gán cho biến:

```
var firstName = 'Group';
var lastName = 'VNP';


var person = {
  firstName: 'Gia Hao',
  lastName: 'Nguyen',
  showName: function() {
    console.log(this.lastName + ' ' + this.firstName);
  }
};

// gán phương thức cho 1 biến:
var x = person.showName;
x(); //VNP Group
// Dữ liệu là các biến toàn cục => this ở đây tham chiếu đến [object Window]
```
giải quết:
```
var x = person.showName.bind(person);
x(); //Nguyen Gia Hao
```
## Prototype

## Sử lý bất đồng bộ


