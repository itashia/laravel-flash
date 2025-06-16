# Laravel Flash Message

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/laravel-flash.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-flash)
![run-tests](https://github.com/spatie/laravel-flash/workflows/run-tests/badge.svg)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/laravel-flash.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-flash)

A lightweight and expressive package to flash temporary messages in Laravel apps. Flash messages are stored in the session and displayed once on the next request.

> **Note**: Only one flash message is supported at a time.

## Example Usage

```php
class MyController
{
    public function store()
    {
        // …

        flash('Data saved successfully!', 'success');

        return back();
    }
}
```

### In your Blade view:

```blade
@if (flash()->message)
    <div class="{{ flash()->class }}">
        {{ flash()->message }}
    </div>
@endif
```

---

## Installation

Install via Composer:

```bash
composer require spatie/laravel-flash
```

---

## API Usage

### Basic Flash Message

```php
flash('Your post was published!');
```

### With CSS Classes

You can pass a string or an array as the second parameter:

```php
flash('Profile updated', 'alert-success');

flash('Validation failed', ['alert', 'alert-danger']); // Will be joined: "alert alert-danger"
```

### Fluent Interface with Meta Data

```php
flash('New order received', 'alert-info')->withMeta(['order_id' => 1234]);
```

You can access meta data in views or logic:

```php
flash()->getMeta('order_id');
```

---

## Defining Custom Levels

You can define message levels using `Flash::levels()` in a service provider:

```php
\Spatie\Flash\Flash::levels([
    'success' => 'bg-green-500 text-white',
    'error'   => 'bg-red-500 text-white',
    'warning' => 'bg-yellow-500 text-black',
]);
```

Then use:

```php
flash()->success('Everything went well!');
flash()->error('Something broke');
```

Each method automatically sets the corresponding `class` and `level`.

---

## Blade Example with Level and Meta

```blade
@if (flash()->message)
    <div class="{{ flash()->class }}">
        {{ flash()->message }}

        @if(flash()->level === 'error')
            <strong>There was an error.</strong>
        @endif

        @if(flash()->hasMeta('order_id'))
            Order ID: {{ flash()->getMeta('order_id') }}
        @endif
    </div>
@endif
```

---

## Macro Support

Register reusable flash types using `macro()`:

```php
use Spatie\Flash\Message;

\Spatie\Flash\Flash::macro('info', function (string $message) {
    return $this->flashMessage(Message::make($message, 'info-class', 'info'));
});
```

Use it like:

```php
flash()->info('Heads up! Something you should know.');
```

---

## Testing

```bash
composer test
```

---

## Alternatives

* [Laracasts/flash](https://github.com/laracasts/flash)
* [Coderello/laraflash](https://github.com/coderello/laraflash)

---

## Postcardware

You're free to use this package, but if it makes it to your production environment, please consider sending us a postcard from your hometown.

**Address:** Spatie, Kruikstraat 22, 2018 Antwerp, Belgium.
We publish all received postcards on [our website](https://spatie.be/en/opensource/postcards).

---

## License

This package is licensed under the MIT License. See [License File](LICENSE.md) for more details.
