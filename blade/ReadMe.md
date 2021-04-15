<!-- omit in toc -->
# Blade Style Guide

<!-- omit in toc -->
## Table of Contents
- [Coding Style](#coding-style)
- [Layouts](#layouts)
- [Utilities](#utilities)
- [Presenter](#presenter)

## Coding Style
- Use soft-tabs with a four space indent.
- Never leave trailing whitespace.
- End each file with a blank newline.
- Use spaces around operators, after commas, and colons, after `{{` and before `}}`.
  ```Blade
  {{ $exists ? 'Foo' : 'Bar' }}
  ```
- No spaces after `(`, `[` or before `]`, `)`.
  ```Blade
  {{ $foo->bar('baz') ?? $bar['baz] }}
  ```
- Never indent within loops and conditionals
  ```Blade
  @foreach($foo as $bar)
  {{ $bar->baz() }}
  @endforeach

  @isset($baz)
  {{ $baz }}
  @endisset
  ```

## Layouts
Use components with `slots` instead of `yield()`
```Blade
<x-layouts.app>
    <x-slot name="header">
        ...
    </x-slot>

    <x-slot name="footer">
        ...
    </x-slot>
    
    ...
</x-layouts.app>
```

## Utilities
- Use anonymous components
- Prefer `slots` rather than `props`
- Add `$attributes`
- Do not define any margin to the outer element
- Make your components as small and abstract as possible
```Blade
{{-- input.blade.php --}}

<input {{ $attributes->merge(['class' => 'font-sans text-base px-2 py-1']) }}>
```

```Blade
{{-- label.blade.php --}}

<label {{ $attributes->merge(['class' => 'font-serif text-base leading-tight']) }}>
    {{ $slot }}
</label>
```

```Blade
{{-- textfield.blade.php --}}

@props(['id'])

<div {{ $attributes->merge(['class' => 'flex space-x-4']) }}>
    <x-label :for="$id">
        {{ $slot }}
    </x-label>
    <x-input type="text" :id="$id">
</div>
```

## Presenter
- Namespace by its type
- Represents one entity
- Do not provide `slots`
```Blade
<x-cards.blogpost :post="$post" />
```

```Blade
<x-articles.blogpost :post="$post" />
```

