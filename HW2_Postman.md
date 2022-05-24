## Endpoint_1

**http://162.55.220.72:5005/first**
1. Отправить запрос. (GET)

ответ:
>  This is the first responce from server!
2. Статус код 200

``` bash 
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```

3. Проверить, что в body приходит правильный string.
``` bash
pm.test("BodyString", function () {
    pm.response.to.have.body("This is the first responce from server!");
});
```
## Endpoint_2

**http://162.55.220.72:5005/object_info_3**

1. Отправить запрос. (POST)

ответ:
> {
    "age": "34",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "u_salary_1_5_year": 8000
    },
    "name": "Viktoria",
    "salary": 2000
}

2. Статус код 200
``` bash
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
``` bash
const JsonData = pm.response.json();
```
4. Проверить, что name в ответе равно name c request (name вбить руками.)
``` bash
let respName0 = JsonData.name

pm.test("RespName=ReqName", function () {
    pm.expect(respName0).to.eql("Viktoria");
});
```
5. Проверить, что age в ответе равно age c request (age вбить руками.)

```bash
let respAge0 = JsonData.age

pm.test("RespAge=ReqAge", function () {
    pm.expect(respAge0).to.eql("34");
});
```
6. Проверить, что salary в ответе равно salary c request (salary вбить руками.)
```bash
let respSalary0 = JsonData.salary

pm.test("RespSalary = ReqSalary", function () {
    pm.expect(respSalary0).to.eql(2000);
});
```
7. Спарсить request.
``` bash
const reqBody = pm.request.body.formdata.toObject()
```
8. Проверить, что name в ответе равно name c request (name забрать из request.)

```bash
let respName1 = JsonData.name
let reqName1 = reqBody.name

pm.test("RespName=ReqName", function () {
    pm.expect(respName1).to.eql(reqName1);
});
```
9. Проверить, что age в ответе равно age s request (age забрать из request.)
```bash
let respAge1 = JsonData.age
let reqAge1 = reqBody.age

pm.test("RespAge = ReqAge", function () {
    pm.expect(respAge1).to.eql(reqAge1);
});
```
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```bash
let respSalary1 = JsonData.salary
let reqSalary1 = reqBody.salary

pm.test("RespAge = ReqAge", function () {
    pm.expect(respSalary1).to.eql(+(reqSalary1));
});
```
11. Вывести в консоль параметр family из response.
```bash
let consoleFamily = JsonData.family
console.log (consoleFamily)
```
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```bash
let respSalary4 = JsonData.family.u_salary_1_5_year
let reqSalary4 = reqBody.salary*4

pm.test("Salary_1.5 year", function () {
    pm.expect(respSalary4).to.eql(reqSalary4);
});
```

## Endpoint_3

**http://162.55.220.72:5005/object_info_3**

1. Отправить запрос. (GET)
ответ:
> {
    "age": "34",
    "family": {
        "children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        "pets": {
            "cat": {
                "age": 3,
                "name": "Sunny"
            },
            "dog": {
                "age": 4,
                "name": "Luky"
            }
        },
        "u_salary_1_5_year": 8000
    },
    "name": "Viktoria",
    "salary": 2000
}

2. Статус код 200
```bash
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```bash
const JsonData = pm.response.json();
```
4. Спарсить request.
```bash
const reqParams = pm.request.url.query.toObject()
```
5. Проверить, что name в ответе равно name c request (name забрать из request.)
```bash
let respName2 = JsonData.name
let reqName2 = reqParams.name;

pm.test("NameResp=NameReq", function () {
    pm.expect(respName2).to.eql(reqName2);
});
```
6. Проверить, что age в ответе равно age s request (age забрать из request.)
```bash
let respAge2 = JsonData.age
let reqAge2 = reqParams.age;

pm.test("AgeResp=AgeReq", function () {
    pm.expect(RespAge2).to.eql(ReqAge2);
});
```
7. Проверить, что salary в ответе равно salary c request (salary забрать из request.)
```bash
let respSalary2 = JsonData.salary;
let reqSalary2 = reqParams.salary;

pm.test("SalaryResp=SalaryReq", function () {
    pm.expect(respSalary2).to.eql(+(reqSalary2));
});
```
8. Вывести в консоль параметр family из response.
```bash
let familyConsole1 = JsonData.family
console.log (familyConsole1)
```
9. Проверить, что у параметра dog есть параметры name.
```bash
let dogName = JsonData.family.pets.dog
pm.test("Param dog have param name", function () {
    pm.expect(dogName).to.have.property("name");
});
```
10. Проверить, что у параметра dog есть параметры age.
```bash
let dogAge = JsonData.family.pets.dog
pm.test("Param dog have param age", function () {
    pm.expect(dogAge).to.have.property("age");
});
```
11. Проверить, что параметр name имеет значение Luky.
```bash
let dogValue_name = JsonData.family.pets.dog.name
pm.test("Param name have value Luky", function () {
    pm.expect(dogValue).to.deep.equal("Luky")
});
```
12. Проверить, что параметр age имеет значение 4.
```bash
let dogValue_age = JsonData.family.pets.dog.age
pm.test("Param age have value 4", function () {
    pm.expect(dogValue_age).to.deep.equal(4)
});
```

## Endpoint_4

**http://162.55.220.72:5005/object_info_4**

1. Отправить запрос. (GET)

ответ:
> {
    "age": 34,
    "name": "Viktoria",
    "salary": [
        2000,
        "4000",
        "6000"
    ]
}
2. Статус код 200
```bash
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```bash
const JsonData = pm.response.json();
```
4. Спарсить request.
```bash
const reqParams = pm.request.url.query.toObject()
```
5. Проверить, что name в ответе равно name c request (name забрать из request.)
```bash
let respName3 = JsonData.name
let reqName3 = reqParams.name;

pm.test("NameResp=NameReq", function () {
    pm.expect(respName3).to.eql(reqName3);
});
```
6. Проверить, что age в ответе равно age из request (age забрать из request.)
```bash
let respAge3 = JsonData.age
let reqAge3 = reqParams.age;

pm.test("NameResp=NameReq", function () {
    pm.expect(respAge3).to.eql(+(reqAge3));
});
```
7. Вывести в консоль параметр salary из request.
```bash
let salaryReq = reqParams.salary
console.log (salaryReq)
```
8. Вывести в консоль параметр salary из response.
```bash
let salaryResp = JsonData.salary
console.log (salaryResp)
```
9. Вывести в консоль 0-й элемент параметра salary из response.
```bash
let salaryReq0 = JsonData.salary[0]
console.log (salaryReq0)
```
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
```bash
let salaryReq1 = JsonData.salary[1]
console.log (salaryReq1)
```
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
```bash
let salaryReq2 = JsonData.salary[2]
console.log (salaryReq2)
```

12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
```bash
let countSalaryResp = JsonData.salary[0]
let countSalaryReq = reqParams.salary

pm.test("CountSalaryResp=CountSalaryReq", function () {
    pm.expect(countSalaryResp).to.deep.eql(+(countSalaryReq));
});
```
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
```bash
let countSalaryResp1 = JsonData.salary[1]
let countSalaryReq1 = reqParams.salary*2

pm.test("CountSalaryResp1=CountSalaryReq1", function () {
    pm.expect(+(countSalaryResp1)).to.deep.eql(+(countSalaryReq1));
});
```
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
```bash
let countSalaryResp2 = JsonData.salary[2]
let countSalaryReq2 = reqParams.salary*3

pm.test("CountSalaryResp2=CountSalaryReq2", function () {
    pm.expect(+(countSalaryResp2)).to.deep.eql(+(countSalaryReq2));
});
```
15. Создать в окружении переменную name
```bash
let User_name = JsonData.name
```
16. Создать в окружении переменную age
```bash
let User_age = JsonData.age
```
17. Создать в окружении переменную salary
```bash
let User_salary = JsonData.salary
```
18. Передать в окружение переменную name
```bash
pm.environment.set("name", User_name);
```
19. Передать в окружение переменную age
```bash
pm.environment.set("age", User_age);
```
20. Передать в окружение переменную salary
```bash
pm.environment.set("salary", User_salary);
```
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```bash
let salary = JsonData.salary
let element = 0
while (element<salary.length) {
    console.log (salary[element])
    element++
}
```

## Endpoint_5

**http://162.55.220.72:5005/user_info_2**

1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос. (POST)

ответ:
>{
    "person": {
        "u_age": 34,
        "u_name": [
            "Viktoria",
            2000,
            34
        ],
        "u_salary_5_years": 8400.0
    },
    "qa_salary_after_1.5_year": 6600.0,
    "qa_salary_after_12_months": 5400.0,
    "qa_salary_after_3.5_years": 7600.0,
    "qa_salary_after_6_months": 4000,
    "start_qa_salary": 2000
}
5. Статус код 200
```bash
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```
6. Спарсить response body в json.
```bash
const JsonData = pm.response.json();
```
7. Спарсить request.
```bash
const reqBody = pm.request.body.formdata.toObject()
```
8. Проверить, что json response имеет параметр start_qa_salary
```bash
pm.test("CheckStart_salary", function () {
    pm.expect(JsonData).to.have.property("start_qa_salary");
});
```
9. Проверить, что json response имеет параметр qa_salary_after_6_months
```bash
pm.test("CheckSalary_6", function () {
    pm.expect(JsonData).to.have.property("qa_salary_after_6_months");
});
```
10. Проверить, что json response имеет параметр qa_salary_after_12_months
```bash
pm.test("CheckSalary_12", function () {
    pm.expect(JsonData).to.have.property("qa_salary_after_12_months");
});
```
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
```bash
pm.test("CheckSalary_1.5", function () {
    pm.expect(JsonData).to.have.property("qa_salary_after_1.5_year");
});
```
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
```bash
pm.test("CheckSalary_3.5", function () {
    pm.expect(JsonData).to.have.property("qa_salary_after_3.5_years");
});
```
13. Проверить, что json response имеет параметр person
```bash
pm.test("person availability", function () {
    pm.expect(JsonData).to.have.property("person");
});
```
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
```bash
let startResp = JsonData.start_qa_salary
let startReq = reqBody.salary
pm.test("Start_salary", function () {
    pm.expect(startResp).to.eql(startReq);
});
```
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
```bash
let salary6Resp = JsonData.qa_salary_after_6_months
let salary6Req = reqBody.salary*2
pm.test("Salary_6", function () {
    pm.expect(salary6Resp).to.eql(salary6Req);
});
```
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
```bash
let salary12Resp = JsonData.qa_salary_after_12_months
let salary12Req = reqBody.salary*2.7
pm.test("Salary_12", function () {
    pm.expect(salary12Resp).to.eql(salary12Req);
});
```
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
```bash
let salary18Resp = JsonData["qa_salary_after_1.5_year"]
let salary18Req = reqBody.salary*3.3
pm.test("Salary_18", function () {
    pm.expect(salary18Resp).to.eql(salary18Req);
});
```
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
```bash
let salary42Resp = JsonData["qa_salary_after_3.5_year"]
let salary42Req = reqBody.salary*3.8
pm.test("Salary_42", function () {
    pm.expect(salary42Resp).to.eql(salary42Req);
});
```
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
```bash
let u_nameResp = JsonData.person.u_name[1]
let salaryReq = reqBody.salary
pm.test("Salary_u_name", function () {
    pm.expect(u_nameResp).to.eql(+(salaryReq));
});
```
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
```bash
let u_ageResp = JsonData.person.u_age
let ageReq = reqBody.age
pm.test("Age_u_age", function () {
    pm.expect(u_ageResp).to.eql(+(ageReq));
});
```

21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
```bash
let u_salResp = JsonData.person.u_salary_5_years
let salReq = reqBody.salary*4.2
pm.test("u_salary5", function () {
    pm.expect(u_salResp).to.eql(salReq);
});
```

22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
