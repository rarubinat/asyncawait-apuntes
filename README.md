# Async/Await en Jquery y ajax



Funci贸n mediante ajax:
```
function myAjax() {
  $.ajax({
    url: ajaxurl,
    type: 'POST',
    data: {
      stuff: 'here',
    },
    success: function (data) {
      //Las locas respuestas de las peticiones anidadas van aqu铆
      var response = data
    },
    error: function (jqXHR, textStatus, errorThrown) {
      // Vacio casi siempre 馃槅
    },
  })
  return response
}
```
Si partimos del anterior c贸digo, un ejemplo de async/await con ajax podr铆a ser:
```
async function myAjax(param) {
  const result = await $.ajax({
    url: ajaxurl,
    type: 'POST',
    data: param,
  })
  return result
}
```
Y es en el return donde devolvemos el resultado de la petici贸n si no hubiera errores. Para capturar los errores podemos hacer lo siguiente:
```
async function myAjax(param) {
  let result
  try {
    result = await $.ajax({
      url: ajaxurl,
      type: 'POST',
      data: param,
    })
    return result
  } catch (error) {
    console.error(error)
  }
}
```
驴Como se resume esta funci贸n? As铆:
```
// En otra parte del c贸digo, dentro de una funci贸n as铆ncrona
const data = await myAjax()
```
Otra opci贸n ser铆a usar promesas:
```
myAjax().then((data) => {
  console.info('Response:', data)
})
```
