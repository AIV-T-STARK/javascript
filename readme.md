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

## Prototype

## Sử lý bất đồng bộ


