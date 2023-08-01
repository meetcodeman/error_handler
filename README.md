# ErrorHandler Module for Ruby on Rails

The `ErrorHandler` module provides a centralized way to handle errors and exceptions in a Ruby on Rails application and return consistent JSON responses with relevant error information. It includes custom error classes and corresponding `rescue_from` blocks to handle specific types of errors.

## Features

- Consistent JSON error responses with status codes, error messages, and exception details.
- Handling of custom errors and common ActiveRecord errors, such as `RecordInvalid`, `RecordNotUnique`, and `RecordNotFound`.
- Eager loading of `CustomError` attributes to set default values for `status`, `code`, and `message`.

## How to Use

1. Copy the `ErrorHandler` module code and paste it into a new file named `error_handler.rb` in the `app/concerns` directory of your Ruby on Rails application.

2. In your `ApplicationController`, include the `ErrorHandler` module using the `include` keyword:

```ruby
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  include ErrorHandler
  # Other ApplicationController code
end
```
The ErrorHandler module will now be available in all controllers that inherit from ApplicationController, enabling centralized error handling and consistent JSON responses.
Custom Errors
The module includes a CustomError class that allows you to create custom error instances with default values for status, code, and message. You can extend this class to create specific custom errors for your application.


## Custome Error
The module includes a CustomError class that allows you to create custom error instances with default values for status, code, and message. You can extend this class to create specific custom errors for your application.

Example:

```ruby
class MyCustomError < ErrorHandler::CustomError
  def initialize
    super(:unprocessable_entity, 422, 'Custom error message')
  end
end
```

## ActiveRecord Errors
The module provides handling for common ActiveRecord errors, such as `RecordInvalid`, `RecordNotUnique`, and `RecordNotFound`. These errors are rescued and appropriate JSON responses are returned.

## Constants
The module defines `ERROR_CODES` and `ERROR_MESSAGES` constants for frequently used HTTP status codes and messages. These constants can be customized as per your application's needs.
