Setuptools helpers for rust Python extensions.

Compile and distribute Python extensions written in rust as easily as if they were written in C.

## Example

### setup.py

```python
from setuptools import setup
from setuptools_rust import RustExtension

setup(name='hello-rust',
    version='1.0',
    rust_extensions=[RustExtension('hello_rust._hello_rust', 'extensions/Cargo.toml')],
    packages=['hello_rust'],
    # rust extensions are not zip safe, just like C-extensions.
    zip_safe=False
)
```

You can use same commands as for c-extensions. For example::

```
>>> python ./setup.py develop
running develop
running egg_info
writing hello-rust.egg-info/PKG-INFO
writing top-level names to hello-rust.egg-info/top_level.txt
writing dependency_links to hello-rust.egg-info/dependency_links.txt
reading manifest file 'hello-rust.egg-info/SOURCES.txt'
writing manifest file 'hello-rust.egg-info/SOURCES.txt'
running build_ext
running build_rust
cargo build --manifest-path extensions/Cargo.toml --features python27-sys
    Finished debug [unoptimized + debuginfo] target(s) in 0.0 secs

Creating /.../lib/python2.7/site-packages/hello-rust.egg-link (link to .)

Installed hello-rust
Processing dependencies for hello-rust==1.0
Finished processing dependencies for hello-rust==1.0
```

Or you can use commands like `bdist_wheel` or `bdist_egg`
