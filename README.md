#http://162.55.220.72:5005/first#
Отправить запрос.
Статус код 200
Проверить, что в body приходит правильный string.
' let testResult = 'This is the first responce from server!'
pm.test("test_1", function () {
    pm.expect(testResult).to.be.a('String');
}); '
