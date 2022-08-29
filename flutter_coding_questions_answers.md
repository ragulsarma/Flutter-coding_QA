# Coding Questions

#### 1. In the below code, list1 declared with var, list2 with final and list3 with const. What is the difference between these lists? Will the last two lines compile?

var list1 = ['I', '💙', 'Flutter'];
final list2 = list1;
list2[2] = 'Dart'; // will this line compile ?
const list3 = list1; // will this line compile ?
##### Answer:
###### Difference between these lists ?
  List1 is Var type   -> The var keyword is used to declare a variable.The Dart compiler automatically knows the type of data based on the assigned to the variable.
  List2 is Final type -> Value must be known at run-time, Can't be changed after initialized. Any variables that isn't known at compile time should be a final variable.
  List2 is const type -> Value must be known at compile-time. If the value you have is calculating at runtime, you can not use a const for it. 
                         This const value can't be changed after initialized.
                             
###### Will the last two lines compile?
###### list2[2] = 'Dart';
This line will be compiled successfully. since list2 is final.
Final - means you can't use the operator = . But you can add (either using = operator or by using word .add) and remove items to the list. The assignment is final, however, the values are NOT constant.
###### const list3 = list1;
This line will not be compiled. As i mentioned earlier const type variables are known at compile time value but here we are trying to assign var type list to 
const type list which wont be compiled. The reason is If the value you have is computed at runtime you can not use a const for it.


#### 2. Identify the problem in the following code. 
String longOperationMethod() {
      var counting = 0;
      for (var i = 1; i <= 1000000000; i++) {
      counting = i;
      }
      return '$counting! times print the value!';
      }

##### Answer:
   Here, we're trying to run the loop over one billion counts its really over killing or expensive task for the system also it blocks our app completely.
   The best solution is to run this method in a different isolate.
```sh
   Future<String> runAndCountLongOperation() async {
     return await compute(longOperationMethod, 1000000000);
   }
```
```sh
   String longOperationMethod(int toValue) {
     var counting = 0;
     for (var i = 1; i <= toValue; i++) {
     counting = i;
     }
     return '$counting! times I print the value!';
   }
```

#### 3. Mobx vs Provider ? Can we use both together ? Write code to demonstrate it.
##### Answer:
Provider is great as your application scales in size. It solves the Store dependency issue very nicely, 
whereas MobX solves the issue around reactivity and ensuring the UI updates as the Store changes.
if you use Observer widget from the mobx_flutter package they track and receive changes when observables change automatically.
At that point you are using Provider to look up a reference to an object (dependency injection).

###### Can we use both together?
Yes. we can use both together.
Mobx + Provider => the Provider package allows us to inject our store and retrieve them anywhere from our widget tree.
we need to inject our Mobx store in our widget tree using Provider.
###### Example code:

```sh
   void main() {
   runApp(MultiProvider(providers: [
   Provider<ThemeStore>(
   create: (_) => ThemeStore(),
   )
   ], child: MobxUsedApp()));
   }
```
```sh
   class MobxUsedApp extends StatelessWidget {
   @override
   Widget build(BuildContext context) {
   return Observer(builder: (context) {
   return MaterialApp(
   title: 'Mobx Management',
   theme: context.watch<ThemeStore>().currentThemeData,
   home: HomePage(),
   );
   });
   }
   }
```
