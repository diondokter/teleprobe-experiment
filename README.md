# Teleprobe experiment

Let's see how easy teleprobe is to use.

Install with:

```sh
cargo install teleprobe --git https://github.com/embassy-rs/teleprobe.git
```
(As of writing there's no real crates.io release yet)

Then run in this root project folder:

```sh
teleprobe server
```

This then uses the config file. This needs to know about the probes it's connected to and how to auth any incoming
connections.
The auth can be oidc or just a string token.

Then to run a test you need to set two environment variables:

```ps1
$Env:TELEPROBE_HOST = "http:/127.0.0.1:8080"
$Env:TELEPROBE_TOKEN = "hN6e2msKlqsW9smsjyF5I7xmiuPQij0O"
```

Then just go to the test you want to run and run it, e.g. with

```sh
cargo run --bin timer
```

If the program ends with a bkpt, then this returns exit code 0.
If the program panics, it'll print out everything and return with exit code 1.

Note that the programs are linked to be run in ram. Teleprobe can handle that.
But it also handles it from flash.

Note that the programs have in them:
```rust
teleprobe_meta::target!(b"nrf52840-dk");
```

This lets teleprobe server deduce which target it needs to use.
This is the name of the target in the config.
