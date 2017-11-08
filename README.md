Designing an API using RAML and Mulesoft Anypoint Studio
=====================================
The purpose of this small project is to design a Customer API using RAML.

## Design Considerations

The API will be used by mobile devices and therefore must contain features that are light-weight and efficient.
With that in mind, resources that return data were assigned traits that support:
* Caching
* Paging

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

### Data Types

The Customer and Address objects have been defined in their own files so we can further modularize the API. With further development of this API, new objects may want to inherit the properties of a Customer, for example, or include an Address as a field.

### Extension

A very simple extension file `extension.raml` has been created to support a version 2 of this API, which will contain a new `/orders` resource which will be implemented in the future.

## Authors

* **Felipe Caldas** - *Initial work* - [Felipe Caldas](https://github.com/felipecaldas)

## License

This project is licensed under the MIT License
