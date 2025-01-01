# Nix Language Basics

- **NOTE:** Everything is an **expression** in nix Language
- **NOTE:** Values in Nix are **immutable**

## Types in Nix

- Integer
- Floating point
- String
- Path
- Boolean

## Identifier naming

- Common language naming convention is applied
- Additionally "-" can be used for naming

```nix
nix-repl> hello-world = "hello world"
```

## String

- String literals can be defined using `"string"` or `''string''`
- Nix expressions can be interpolated within strings using `${}` syntax

Ex:-

```nix
nix-repl> name = "Srinesh"
nix-repl> welcome-message = "Welcome ${name}"
nix-repl> welcome-message
# "Welcome Srinesh"
```

Ex:-

```nix
nix-repl> result = 60
nix-repl> "You are ${if result < 50 then "fail" else "pass"}"
# "You are passed"
```

### Escaping `${...}`

- When using `""`, `${}` can be escaped with `\`
- when using `''''`, `${}` can be escaped with `''`

Ex:-

```nix
nix-repl> name = "Srinesh"
nix-repl> "${name}"
# Srinesh
nix-repl> "\${name}"
# ${name}

nix-repl> ''${name}''
# Srinesh
nix-repl> ''''${name}''
# ${name}
```

## Lists

NOTE: Adding and removing from a list is possible but will return a new list
since everything is mutable in nix.

- Lists can be defined withing square brackets
- List items are separated by space

Ex:-

```nix
nix-repl> [1 "hello" /home]
# [1 "hello" /home]
```

## Attribute Set

```nix
s = { foo = "bar"; a-b = "baz"; "123" = "num"; }
```
