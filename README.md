1- TypeScript-এ Interface এবং Type এর মধ্যে কী কী পার্থক্য আছে?
<br>
ans : TypeScript-এ interface এবং type alias—দুটোই object এর structure নির্ধারণ করতে ব্যবহৃত হয়, কিন্তু কিছু গুরুত্বপূর্ণ পার্থক্য রয়েছে:

** Extension/Inheritance
-> Interface: এক বা একাধিক interface কে extends করতে পারে।
-> Type: type alias intersection (&) ব্যবহার করে অন্যান্য type এর সাথে মিক্স করা যায়।

উদাহরণ:
ts
```
interface A { name: string }
interface B extends A { age: number }

type X = { name: string }
type Y = X & { age: number }

```

** Declaration Merging (ঘোষণা একত্রিত হওয়া)
-> Interface: একই নামে দুইটি interface লিখলে TypeScript এগুলোকে merge করে।
-> Type: type alias কোনোভাবেই merge হয় না।

উদাহরণ:
ts
```
interface User { name: string }
interface User { age: number }
// Output: { name: string; age: number }

```

** Primitive, Union & Tuple সাপোর্ট
-> Interface: কেবলমাত্র object structure এর জন্য ভালো।
-> Type: primitive, union, intersection, tuple—সবকিছুই represent করতে পারে।

উদাহরণ:
ts
```
type ID = string | number;  // Interface দিয়ে করা যায় না

```
** Implements
-> Interface: class implements করতে পারে।
-> Type: type alias ও class implements করতে পারে — তবে অবজেক্ট স্ট্রাকচারের ক্ষেত্রে বেশি ব্যবহৃত হয়।

** Syntax এবং Use-case Preference
-> Interface: সাধারণত object shape, class contract এবং API structure এর জন্য ব্যবহৃত হয়।
-> Type: complex type operations, union, mapped type, এবং advanced টাইপিং এর জন্য ভালো।


2- TypeScript-এ keyof কীওয়ার্ডের ব্যবহার কী? একটি উদাহরণসহ ব্যাখ্যা করুন।
ans : TypeScript-এর keyof কীওয়ার্ড একটি object type-এর সবগুলো key-এর union type তৈরি করে। অর্থাৎ, কোনো object-এর property নামগুলোকে টাইপ হিসেবে ব্যবহার করতে চাইলে keyof অত্যন্ত উপকারী।

এটি মূলত type-safe access, generic utility functions, এবং object property validation তৈরিতে ব্যবহৃত হয়।

উদাহরণ:
ts
```
interface User {
  name: string;
  age: number;
  email: string;
}

type UserKeys = keyof User;
// Output type: "name" | "age" | "email"

```

এখন UserKeys টাইপটি কেবল "name", "age", অথবা "email"—এই তিনটির কোনো একটি হতে পারে।

আরেকটি বাস্তব উদাহরণ (Generic function):
ts
```
function getValue<T>(obj: T, key: keyof T) {
  return obj[key];
}

const user = { name: "Mahib", age: 22 };

getValue(user, "name"); // valid
getValue(user, "age");  // valid
// getValue(user, "email");  // error (key নেই)

```

এখানে keyof নিশ্চিত করে যে function-এ শুধু object-এ থাকা key-ই পাঠানো যাবে—যার ফলে কোড হয় টাইপ-সেফ।

সংক্ষেপে (ইন্টারভিউ উত্তর):
keyof একটি object type-এর সব property নামকে union type হিসেবে রিটার্ন করে, এবং type-safe object key access নিশ্চিত করতে ব্যবহৃত হয়।
