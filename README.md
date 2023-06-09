# dyn_inject

This crates provides utilities for dependency injection in Rust, also supporting `dyn Trait` trait objects instead of only static, sized types.

# Example

```rs
use dyn_inject::Registry;

trait Foo {
    fn foo();
}

struct Bar;

impl Foo for Bar {
    fn foo() {
        println!("Hello");
    }
}

fn main() {
    let mut registry = Registry::new();
    registry.put_dyn::<dyn Foo>(Bar);
    // Calls Bar::foo()
    registry.get_dyn::<dyn Foo>().unwrap().foo()
}
```