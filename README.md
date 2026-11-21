<img src="assets/logo.png" width="112" height="112" alt="A crested grebe spreads its chestnut cheek ruff above the water.">

# Grebe

Build a repeatable keyset page and return the exact next cursor. This Blyx workflow framework is part of the databases and migrations collection.

Offset pagination on changing data can repeat records. Validate the ordered key and return the final emitted key for the next request. [PostgreSQL, ordered pagination](https://www.postgresql.org/docs/current/queries-limit.html)

## Editor extension

Install **RahulChaube.blyx-grebe** to run the worked example and use the framework’s function completions in a Blyx file. Open an empty `.blyx` file, enter `blyx-grebe-demo`, then choose **Blyx: Run File**. [Editor downloads](https://www.blyx-lang.space/packages/grebe#editor) · [Download the extension](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-grebe-0.1.0.vsix) · [Starter with framework source](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-grebe-starter-0.1.0.zip)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-grebe.git
cd blyx-grebe
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-grebe) · [Package page](https://www.blyx-lang.space/packages/grebe) · [Handbook](https://doc.blyx-lang.space/guide/grebe)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-grebe.git vendor/grebe
```

```blyx
use vendor::grebe::grebe;

fn main() {
    let keys = [10, 20, 30, 40];
    let cursor = 15.0;
    let size = 2.0;
    let result = grebe_page(keys, cursor, size);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
3
30
1
```

## API

`grebe_page(keys, cursor, size)`

Returns [first index, exclusive end, resume key, has more]. On an empty result the input cursor is retained. Supply stable unique numeric keys from a consistent snapshot. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| keys | Vector of values, each a exact signed integer |
| cursor | A exact signed integer |
| size | A positive exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "10,20,30,40" 15 2
```

## Libraries

- [KeyOrders](https://github.com/Rahulchaube1/blyx-keyorders/tree/v0.1.0) — Check a cursor key sequence for repeated and descending adjacent values.
- [PageCursor](https://github.com/Rahulchaube1/blyx-pagecursor/tree/v0.1.0) — Find a keyset page strictly after a cursor in sorted keys.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-grebe/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The [artwork notice](assets/NOTICE.txt) records credits for earlier editions.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
