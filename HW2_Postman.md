## Endpoint_1

**http://162.55.220.72:5005/first**
1. Отправить запрос.
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
