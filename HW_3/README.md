# HW_2 POSTMAN
### Completed requests collection [HW_2.postman_collection.json](https://github.com/Pavlik1100/POSTMAN/blob/main/HW_2/HW_2.postman_collection.json)
### Test run Completed requests collection [HW_2.postman_test_run.json](https://github.com/Pavlik1100/POSTMAN/blob/main/HW_2/HW_2.postman_test_run.json)
#

### 1) необходимо залогиниться и получить токен
`POST`  
`http://162.55.220.72:5005/login`  
`login` : str (кроме /)  
`password` : str  

Приходящий токен необходимо передать во все остальные запросы.  
```javascript
var jsonData = pm.response.json();
var get_token = jsonData.token;
pm.environment.set("token", get_token);
```
#
### 2) http://162.55.220.72:5005/user_info
`req.` (RAW JSON)  
`POST`  
`age`: int  
`salary`: int  
`name`: str  
`auth_token`  

`resp.`
```sh
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```  
#
### Тесты:

   1) Статус код 200
      ```javascript
      pm.test("Status code is 200", function () {
          pm.response.to.have.status(200);
      });
      ```

   2) Проверка структуры json в ответе.
      ```javascript
      const schema = {
          "type": "object",
          "properties": {
              "person": {
                  "type": "object",
                  "properties":{
                      "u_age": {
                          "type": "integer"
                      },
                      "u_name": {
                          "type": "array",
                          "items": [
                              {
                                  "type": "string"
                              },
                              {
                                  "type": "integer"
                              },
                              {
                                  "type": "integer"
                              }
                          ]
                      },
                      "u_salary_1_5_eyar": {
                          "type": "integer"    
                      }            
                  },
                  "required": [
                      "u_age",
                      "u_name",
                      "u_salary_1_5_year"
                  ]
              },
              "qa_salary_after_12_months": {
                  "type": "number"
              },
              "qa_salary_after_6_months": {
                  "type": "integer"
              },
              "start_qa_salary":{
                  "type": "integer"
              }
          },
          "required": [
              "person",
              "qa_salary_after_12_months",
              "qa_salary_after_6_months",
              "start_qa_salary"
          ]
      }

      pm.test("Validate schema", () =>{
          pm.response.to.have.jsonSchema(schema);
      });
      ```
   3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
      ```javascript
      const resData = pm.response.json();
      ```
      `check response qa_salary_after_6_months = salary * 2`
      ```javascript
      pm.test("Check correctly coef salary x2, from response qa_salary_after_6_months", () => {
          pm.expect(resData.person.u_name[1]*2).to.eql(resData.qa_salary_after_6_months);
      });
      ```
      `check response qa_salary_after_12_months = salary * 2.9`
      ```javascript
      pm.test("Check correctly coef salary x 2.9, from response qa_salary_after_12_months", () => {
          pm.expect(resData.person.u_name[1]*2.9).to.eql(resData.qa_salary_after_12_months);
      });
      ```
      `check response u_salary_1.5_eyar = salary * 4`
      ```javascript
      pm.test("Check correctly coef salary x 4, from response u_salary_1_5_year", () => {
          pm.expect(resData.person.u_name[1]*4).to.eql(resData.person.u_salary_1_5_year);
      });
      ```
   4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user
      ```javascript
      pm.environment.set("salary", resData.person.u_salary_1_5_year);
      ```

### 3) http://162.55.220.72:5005/new_data    
   `req.`  
   `POST`  
   `age`: int  
   `salary`: int  
   `name`: str  
   `auth_token`  

   `response`
   ```sh
   {'name':name,
     'age': int(age),
     'salary': [salary, str(salary*2), str(salary*3)]}
   ```
#
### Тесты:
   1) Статус код 200
      ```javascript
      pm.test("Status code is 200 ok", () => {
          pm.response.to.have.status(200);
      });
      ```
   2) Проверка структуры json в ответе.
      ```javascript
      const schema = {
          "type": "object",
          "properties": {
              "age": {
                  "type": "integer"
              },
              "name": {
                  "type": "string"
              },
              "salary": {
                  "type": "array",
                  "items": [
                      {
                          "type": "integer"
                      },
                      {
                          "type": "string"
                      },
                      {
                          "type": "string"
                      }
                  ]
              }
          },
          "required": [
              "age",
              "name",
              "salary"
          ]
      };

      pm.test("Validate schema ok", () => {
          pm.response.to.have.jsonSchema(schema)
      }); 
      ```
   3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
      ```javascript
      const resData = pm.response.json();
      ```
      `check response salary[1]=salary*2`
      ```javascript
      pm.test("Check correctly coef =2, from response salary[1]", () => {
          pm.expect(parseInt(resData.salary[1])).to.eql(resData.salary[0]*2)
      });
      ```
      `check response salary[2]=salary*3`
      ```javascript
      pm.test("Check correctly coef = 3, from response salary[2]", () => {
          pm.expect(parseInt(resData.salary[2])).to.eql(resData.salary[0]*3)
      });
      ```
   4) проверить, что 2-й элемент массива salary больше 1-го и 0-го
      ```javascript
      pm.test("Check that salary[1] > salary[0]", () => {
          if (parseInt(resData.salary[0])>=parseInt(resData.salary[1])) {
          pm.expect.fail();
          }
      });
      ```
### 4) http://162.55.220.72:5005/test_pet_info
   `req.`  
   `POST`  
   `age`: int  
   `weight`: int  
   `name`: str  
   `auth_token`  
  `response`
  ```sh
  {'name': name,
   'age': age,
   'daily_food':weight * 0.012,
   'daily_sleep': weight * 2.5}
   ```
   #
   ### Тесты:
   1) Статус код 200
      ```javascript
      pm.test("Status code is 200 ok", () => {
          pm.response.to.have.status(200);
      });
      ```
   2) Проверка структуры json в ответе.
      ```javascript
      const schema = {
          "type": "object",
          "properties": {
              "age": {
                  "type": "integer"
              },
              "daily_food": {
                  "type": "number"
              },
              "daily_sleep": {
                  "type": "number"
              },
              "name": {
                  "type": "string"
              }
          },
          "required": [
              "age",
              "daily_food",
              "daily_sleep",
              "name"
          ]
      };

      pm.test("Validate scheme of response", () => {
          pm.response.to.have.jsonSchema(schema)
      });
      ```
   3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.
      ```javascript
      const resData = pm.response.json();
      const reqData = request.data;
      ```
      `check response daily_food = weight * 0.012`
      ```javascript
      pm.test("Check correct coef daily_food from response, daily_food = weight * 0.012", () => {
         pm.expect(reqData.weight*0.012).to.eql(resData.daily_food)
      });
      ```
      `check response daily_sleep = weight * 2.5`
      ```javascript
      pm.test("Check correct coef daily_sleep from response,  daily_sleep = weight * 2.5", () => {
      pm.expect(reqData.weight*2.5).to.eql(resData.daily_sleep)
      });
      ```
### 5) http://162.55.220.72:5005/get_test_user
   `req.`
   `POST`
   `age`: int
   `salary`: int
   `name`: str
   `auth_token`

   `response`
   ```sh
   {'name': name,
    'age':age,
    'salary': salary,
    'family':{'children':[['Alex', 24],['Kate', 12]],
    'u_salary_1.5_year': salary * 4}
     }
   ```
   #
   ### Тесты:
   1) Статус код 200
      ```javascript
      pm.test("Status code is 200 ok", () => {
          pm.response.to.have.status(200);
      });
      ```
   2) Проверка структуры json в ответе.
      ```javascript
      const schema = {
          "type": "object",
          "properties": {
              "age": {
                  "type": "string"
              },
              "family":{
                  "type": "object",
                  "properties": {
                      "children": {
                          "type": "array",
                          "items":[
                              {
                                  "type": "array",
                                  "items": [
                                      {
                                          "type": "string"
                                      },
                                      {
                                          "type": "integer"
                                      }
                                  ]
                              },
                              {
                                  "type": "array",
                                  "items": [
                                      {
                                          "type": "string"
                                      },
                                      {
                                          "type": "integer"
                                      }
                                  ]
                              }
                          ]
                      },
                      "u_salary_1_5_year": {
                          "type": "integer"
                      }
                  },
                  "required": [
                      "children",
                      "u_salary_1_5_year"
                  ]
              },
              "name": {
                  "type": "string"
              },
              "salary": {
                  "type": "integer"
              }
          },
          "required": [
              "age",
              "family",
              "name",
              "salary"
          ]
      };

      pm.test("Validate schema", () => {
          pm.response.to.have.jsonSchema(schema);
      });
      ```
   3) Проверить что занчение поля name = значению переменной name из окружения
      ```javascript
      pm.test("Check 'name' from request field matches variable 'name' from environment", () => {
          pm.expect(pm.environment.get("name")).to.eql(request.data.name);
      });
      ```

   4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age
      ```javascript
      pm.test("Check value field 'age' from response matches value field 'age' from request", () => {
          const resData = pm.response.json();
          pm.expect(request.data.age).to.eql(resData.age);
      });
      ```





# [Back to main dir POSTMAN](https://github.com/Pavlik1100/POSTMAN)
