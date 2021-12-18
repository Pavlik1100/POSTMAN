## HW_2 Postman
1. http://162.55.220.72:5005/first
   1) Отправить запрос.  
      Ззапрос на `http://162.55.220.72:5005/first` с методом `get`, отправляем нажав `send`
   2) Статус код `200`
      ```javascript
      pm.test("Status code is 200", function () {
         pm.response.to.have.status(200);
      });
      ```
   3) Проверить, что в body приходит правильный string.
      ```javascript
      pm.test("Response has desired text", function () {
         pm.expect(pm.response.text()).to.include("This is the first responce from server!");
      });
      ```
   ##
2. http://162.55.220.72:5005/user_info_3
   1. Отправить запрос.  
      Ззапрос на `http://162.55.220.72:5005/user_info_3` с методом `post` и `body` `form-data` с ключами `age`, `name`, `salary`, отправляем нажав `send`
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
      pm.test("Name s request", () => {
         const nameReq = request.data.name;
         pm.expect(jsonData.name).to.eql(nameReq);    
      });
      ```
   5. Проверить, что age в ответе равно age s request (age вбить руками.)
      ```javascript
      pm.test("Age s request", () => {
         const ageReq = request.data.age;
         pm.expect(jsonData.age).to.eql(ageReq);
      });
      ```
   6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
      ```javascript
      pm.test("Salary s request", () => {
         const salaryReq = request.data.salary;
         pm.expect(jsonData.salary).to.eql(parseInt(salaryReq));
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
   ##
3) http://162.55.220.72:5005/object_info_3
   1. Отправить запрос.  
         Ззапрос на `http://162.55.220.72:5005/object_info_3` с методом `get` и `params` с ключами `age`, `name`, `salary`, отправляем нажав `send`
   2. Статус код 200
      ```javascript
      pm.test("Status code is 200", function () {
         pm.response.to.have.status(200);
      });
   3. Спарсить response body в json.
      ```javascript
      const respJson = pm.response.json();
      ```
   4. Спарсить request.
      ```javascript
      let reqJson = {}; 
      pm.request.url.query.all().forEach((param) => {
         reqJson[param.key]=param.value
      });
      ```
   5. Проверить, что name в ответе равно name s request (name забрать из request.)
      ```javascript
      pm.test("Name from response matches Name from request", () => {
         pm.expect(respJson.name).to.eql(reqJson.name);
      });
      ```
   6. Проверить, что age в ответе равно age s request (age забрать из request.)
      ```javascript
      pm.test("Age frim response matches Age from request", () => {
         pm.expect(respJson.age).to.eql(reqJson.age);
      });
      ```
   7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
      ```javascript
      pm.test("Salary from response matches Salary from request", () => {
         pm.expect(respJson.salary).to.eql(parseInt(reqJson.salary));
      });
      ```
   8. Вывести в консоль параметр family из response.
      ```javascript
      console.log(respJson.family);
      ```
   9. Проверить, что у параметра dog есть параметры name.
      ```javascript
      pm.test("Property dog include property name", () => {
         pm.expect(respJson.family.pets.dog).to.have.property("name");
      });
      ```
    10. Проверить, что у параметра dog есть параметры age.
        ```javascript
        pm.test("Property dog include property age", () => {
           pm.expect(respJson.family.pets.dog).to.have.property("age");
        });
        ```   
    11. Проверить, что параметр name имеет значение Luky.
         ```javascript
         pm.test("Property name matchs Luky", () => {
            pm.expect(respJson.family.pets.dog.name).to.eql("Luky");
         });
         ```  
    12. Проверить, что параметр age имеет значение 4.
         ```javascript
         pm.test("Propery age matches 4", () => {
            pm.expect(respJson.family.pets.dog.age).to.eql(4);
         })
         ```
   ##
4) http://162.55.220.72:5005/object_info_4
   1. Отправить запрос.
         Ззапрос на `http://162.55.220.72:5005/object_info_4` с методом `get` и `params` с ключами `age`, `name`, `salary`, отправляем нажав `send`
   2. Статус код 200
      ```javascript
      pm.test("Status code is 200", function () {
         pm.response.to.have.status(200);
      });   
   3. Спарсить response body в json.
      ```javascript
      const respJson = pm.response.json();
      ```
   4. Спарсить request.
      ```javascript
      let reqJson = {}; 
      pm.request.url.query.all().forEach((param) => {
         reqJson[param.key]=param.value
      });
      ```
   5. Проверить, что name в ответе равно name s request (name забрать из request.)
      ```javascript
      pm.test("Name from response matches Name from request", () => {
         pm.expect(jsonRes.name).to.eql(jsonReq.name);
      });
      ```
   6. Проверить, что age в ответе равно age из request (age забрать из request.)
      ```javascript
      pm.test("Age from response matches Age from request", () => {
         pm.expect(parseInt(jsonReq.age)).to.eql(jsonRes.age);
      });
      ```
   7. Вывести в консоль параметр salary из request.
      ```javascript
      console.log(jsonReq.salary);
      ```
   8. Вывести в консоль параметр salary из response.
      ```javascript
      console.log(jsonRes.salary);
      ```
   9. Вывести в консоль 0-й элемент параметра salary из response.
      ```javascript
      console.log(jsonRes.salary[0]);
      ```
   10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
       ```javascript
       console.log(jsonRes.salary[1]);
       ```
   11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
       ```javascript
       console.log(jsonRes.salary[2]);
       ```
   12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
       ```javascript
       pm.test("Property salary[0] from response matches property from salary request", () => {
          pm.expect(parseInt(jsonReq.salary)).to.eql(jsonRes.salary[0]);
       });
       ```
   13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
       ```javascript
       pm.test("Property salary[1] from response matches property from salary request x 2", () => {
          pm.expect(parseInt(jsonReq.salary)*2).to.eql(parseInt(jsonRes.salary[1]));
       });
       ```
   14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
       ```javascript
       pm.test("Property salary[2] from response matches property from request x 3", () => {
          pm.expect(parseInt(jsonReq.salary)*3).to.eql(parseInt(jsonRes.salary[2]));
       });
   15. Создать в окружении переменную name    
       Вкладка `Environments` -> выбираем окружение -> создать переменные `name` -> сохранить окружение
   16. Создать в окружении переменную age  
       Вкладка `Environments` -> выбираем окружение -> создать переменные `age` -> сохранить окружение
   17. Создать в окружении переменную salary  
       Вкладка `Environments` -> выбираем окружение -> создать переменные `salary` -> сохранить окружение
   18. Передать в окружение переменную name
       ```javascript
       const name_res = jsonRes.name;
       pm.environment.set("name", name_res);
       ```
   19. Передать в окружение переменную age
       ```javascript
       const age_res = jsonRes.age;
       pm.environment.set("age", age_res);
       ```
   20. Передать в окружение переменную salary
       ```javascript
       const salary_res = jsonRes.salary[0];
       pm.environment.set("salary", salary_res);
       ```
   21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
       ```javascript
       const list_of_salary = Array.from(jsonRes.salary);

       for (let i=0; i<list_of_salary.length; i += 1) {
          console.log(list_of_salary[i]);
       }
       ```
       или
       ```javascript
       jsonRes.salary.forEach(el => console.log(el));
       ```
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
