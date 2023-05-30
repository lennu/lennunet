---
title: Simple String as JSON from Spring Rest Controller in Kotlin
date: 2020-01-22
redirect_from: /simple-string-as-json-from-spring-rest-controller-in-kotlin/
---
Spring or Spring Boot usually by default transforms items to JSON. However if you return simple String like “cool” then that is not turned into JSON like here.

```
@GetMapping("/cool")
fun cool(): String {
    return "cool"
}
```


In this example it is returned as plain text which makes it hard for the caller to handle because the API was supposed to be JSON API. There are two ways to go around this.

The first method is stringify the text to JSON using Kotlin’s internal stringify method and then return it.

```
@GetMapping("/cool")
fun cool(): String {
    return stringify("cool")
}
```


Or do if you want to automatically do this then you can configure Spring to remove `StringHttpMessageConverter` which is responsible for plain string objects. This was the next converter gets the job and usually this is JSON.

```
// WebMvcConfiguration.kt

@Component
class WebMvcConfiguration : WebMvcConfigurationSupport() {
    override protected fun extendMessageConverters(converters: MutableList<HttpMessageConverter<*>>) {
        converters.stream()
            .filter { c -> c is StringHttpMessageConverter }
            .findFirst().ifPresent(Consumer<HttpMessageConverter<*>> { converters.remove(it) })
    }
}
```
