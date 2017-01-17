### Theme function (`Drupal.theme`)

`Drupal.theme` is the client-side counterpart of the server-side `theme()`-function. All of the server-side `theme()` function has been removed in Drupal 8. The client-side function however remains part of the Javascript API. All markup (defined in Javascript) should go through these theme functions.

The beauty of this system is that it allows the reuse of theme functions as templates and the override of these functions in themes. A module can define a theme function; a theme that wants to change the markup can override the function to define its own template.

The `Drupal.theme` function [has been simplified](https://www.drupal.org/node/1816980).
Previously it was possible to declare functions in `Drupal.theme.prototype`,
where workaround code made `Drupal.theme()` behave as intended. Instead these
Javascript theme functions are now using `Drupal.theme` directly.

***

**Drupal 7:**

    Drupal.theme.prototype.example = function () {
      var markup = '<p>Hello world!</p>';
      return markup;
    };

    Drupal.theme.prototype.anotherExample = function (title, name) {
      var markup = '<p>Hello ' + title + ' ' + name '!</p>';
      return markup;
    };

    var example = Drupal.theme('example'); // <p>Hello world!</p>
    var another_example = Drupal.theme('anotherExample', 'Mr.', 'Dries'); // <p>Hello Mr. Dries!</p>

**Drupal 8:**

    Drupal.theme.example = function () {
      var markup = '<p>Hello world!</p>';
      return markup;
    };

    Drupal.theme.anotherExample = function (title, name) {
      var markup = '<p>Hello ' + title + ' ' + name '!</p>';
      return markup;
    };

    var example = Drupal.theme('example'); // <p>Hello world!</p>
    var another_example = Drupal.theme('anotherExample', 'Mr.', 'Dries'); // <p>Hello Mr. Dries!</p>

#### Declaring several theme functions

Declaring several theme functions can be done using the
[`$.extend()`](http://api.jquery.com/jquery.extend/) pattern. This is a
considered a better approach for declaring serveral functions.

***

    $.extend(Drupal.theme, {
      example: function () { return 'Hello world!'; },
      anotherExample: function (title, name) { return '<p>Hello ' + title + ' ' + name '!</p>'; }
    });

***
