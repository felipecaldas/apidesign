Designing an API using RAML and Mulesoft Anypoint Studio
=====================================
The purpose of this small project is to design a Customer API using RAML.

## Design Considerations

The API will be used by mobile devices and therefore must contain features that are light-weight and efficient.
With that in mind, resources that return data were assigned traits that support:
* Caching
* Paging

By adding paging functionality to resources of the API, mobile consumers can then control how much data they want to be returned. That means that less data will be returned, and not the whole resulset, and therefore making the communication between mobile app and API faster.

The caching functionality was added with the idea that if the data has not changed, there's no reason for the API to return it again.

## Extensibility & Modularization

### Resource Types

The use of `resource types` helps remove repetition throughout the API spec by defining templates on how each resource/verb should look like.
With that, the definition of the /customers resource, become as simple as this:

```
/customers:
  type:
    assets.collection:
      responseExampleVar: !include examples/customers.json
```

The type `assets.collection` defines all the methods that `/customers` requires.

### Traits

The use of `traits` adds new nodes at method level, for example a `paging` enabled method. You can then reuse the trait throughout the specification.

It was also added as HTTP `headers` to the `GET /customers` and `GET /customers/{id}` the notion of `If-None-Match` and `If-Modified-Since`. Both optional. They are:

* If-None-Match - the client can search the API by giving the ETag value associated with the object. If that ETag value has changed, the API will the return the new value, otherwise it won't return the large resulset associated with the object.

* If-Modified-Since - the client can search the API to retrieve records that are newer than an specific date/time.

### Data Types

The Customer and Address objects have been defined in their own files so we can further modularize the API. With further development of this API, new objects may want to inherit the properties of a Customer, for example, or include an Address as a field.

### Extension

A very simple extension file `extension.raml` has been created to support a version 2 of this API, which will contain a new `/orders` resource which will be implemented in the future. By using the extension, we can now baseline our API on version 1, and extend it on version 2, but using version 1 as the parent.

## Authors

* **Felipe Caldas** - *Initial work* - [Felipe Caldas](https://github.com/felipecaldas)

## License

This project is licensed under the MIT License
