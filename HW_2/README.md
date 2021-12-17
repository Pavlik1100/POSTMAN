# POSTMAN
### [HW_1](https://github.com/Pavlik1100/POSTMAN/tree/main/HW_1) - Simple requests collection in Postman 
ДЗ_2 Postman
=====

=====

http://162.55.220.72:5005/first
1. Отправить запрос.
2. Статус код 200
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
3. Проверить, что в body приходит правильный string.
```javascript
pm.test("Response has desired text", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!");
});
```
http://162.55.220.72:5005/user_info_3
1. Отправить запрос.
2. Статус код 200
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```javascript
const jsonData = pm.response.json();
```
4. Проверить, что name в ответе равно name s request (name вбить руками.)
```javascript
pm.test("Name is Pasha", () => {
    pm.expect(jsonData.name).to.eql("Pasha");    
});
```
5. Проверить, что age в ответе равно age s request (age вбить руками.)
```javascript
pm.test("Age is 28", () => {
    pm.expect(jsonData.age).to.eql("28");
});
```
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
```javascript
pm.test("Salary is 1000", () => {
    pm.expect(jsonData.salary).to.eql(1000);
});
```
7. Спарсить request.
```javascript
const jsonData_req = request.data;
```
8. Проверить, что name в ответе равно name s request (name забрать из request.)
```javascript
pm.test("Name from response matches Name from request", () =>{
    pm.expect(jsonData.name).to.eql(jsonData_req.name);    
});
```
9. Проверить, что age в ответе равно age s request (age забрать из request.)
```javascript
pm.test("Age from response matches Age from request", () => {
    pm.expect(jsonData.age).to.eql(jsonData_req.age);
})
```
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```javascript
pm.test("Salary from response matches Salary from request", () => {
    pm.expect(jsonData.salary).to.eql(parseInt(jsonData_req.salary));
})
```
11. Вывести в консоль параметр family из response.
```javascript
console.log(jsonData.family);
```
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```javascript
pm.test("u_salary_1_5_year from response matches salary*4 from request", () => {
    pm.expect(jsonData.family.u_salary_1_5_year).to.eql((jsonData_req.salary)*4);
})
```
http://162.55.220.72:5005/object_info_3
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
8. Вывести в консоль параметр family из response.
9. Проверить, что у параметра dog есть параметры name.
10. Проверить, что у параметра dog есть параметры age.
11. Проверить, что параметр name имеет значение Luky.
12. Проверить, что параметр age имеет значение 4.

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

const respJson = pm.response.json();
console.log(respJson);

let reqJson = {};
pm.request.url.query.all().forEach((param) => {
    reqJson[param.key]=param.value
});

console.log(reqJson);

console.log(reqJson.name  + " " + typeof(reqJson.name));
console.log(respJson.name + " " + typeof(respJson.name));

pm.test("Name from response matches Name from request", () => {
    pm.expect(respJson.name).to.eql(reqJson.name);
});

console.log(reqJson.age  + " " + typeof(reqJson.age));
console.log(respJson.age + " " + typeof(respJson.age));

pm.test("Age frim response matches Age from request", () => {
    pm.expect(respJson.age).to.eql(reqJson.age);
});

console.log(reqJson.salary + " " + typeof(reqJson.salary));
console.log(respJson.salary + " " + typeof(respJson.salary));

pm.test("Salary from response matches Salary from request", () => {
    pm.expect(respJson.salary).to.eql(parseInt(reqJson.salary));
});

console.log(respJson);

pm.test("Property dog include property name", () => {
    pm.expect(respJson.family.pets.dog).to.have.property("name");
});

pm.test("Property dog include property age", () => {
    pm.expect(respJson.family.pets.dog).to.have.property("age");
});

pm.test("Property name matchs Luky", () => {
    pm.expect(respJson.family.pets.dog.name).to.eql("Luky");
});

pm.test("Propery age matches 4", () => {
    pm.expect(respJson.family.pets.dog.age).to.eql(4);
})

http://162.55.220.72:5005/object_info_4
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age из request (age забрать из request.)
7. Вывести в консоль параметр salary из request.
8. Вывести в консоль параметр salary из response.
9. Вывести в консоль 0-й элемент параметра salary из response.
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

const jsonRes = pm.response.json();

let jsonReq = {};
pm.request.url.query.all().forEach((param) => {
    jsonReq[param.key]=param.value
});

console.log(jsonReq);

pm.test("Name from response matches Name from request", () => {
    pm.expect(jsonRes.name).to.eql(jsonReq.name);
});

pm.test("Age from response matches Age from request", () => {
    pm.expect(parseInt(jsonReq.age)).to.eql(jsonRes.age);
});

console.log(jsonReq.salary);

console.log(jsonRes.salary);

console.log(jsonRes.salary[0]);

console.log(jsonRes.salary[1]);

console.log(jsonRes.salary[2]);

pm.test("Property salary[0] from response matches property from salary request", () => {
    pm.expect(parseInt(jsonReq.salary)).to.eql(jsonRes.salary[0]);
});

pm.test("Property salary[1] from response matches property from salary request x 2", () => {
    pm.expect(parseInt(jsonReq.salary)*2).to.eql(parseInt(jsonRes.salary[1]));
});

pm.test("Property salary[2] from response matches property from request x 3", () => {
    pm.expect(parseInt(jsonReq.salary)*3).to.eql(parseInt(jsonRes.salary[2]));
})

http://162.55.220.72:5005/user_info_2
1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос.
5. Статус код 200
6. Спарсить response body в json.
7. Спарсить request.
8. Проверить, что json response имеет параметр start_qa_salary
9. Проверить, что json response имеет параметр qa_salary_after_6_months
10. Проверить, что json response имеет параметр qa_salary_after_12_months
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
13. Проверить, что json response имеет параметр person
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
