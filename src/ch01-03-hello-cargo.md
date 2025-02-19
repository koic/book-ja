<!--
## Hello, Cargo!
-->

## Hello, Cargo!

<!--
Cargo is Rust’s build system and package manager. Most Rustaceans use this tool
to manage their Rust projects because Cargo handles a lot of tasks for you,
such as building your code, downloading the libraries your code depends on, and
building those libraries. (We call libraries your code needs *dependencies*.)
-->

Cargoは、Rustのビルドシステム兼、パッケージマネージャです。ほとんどのRustaceanはこのツールを使用して、
Rustプロジェクトの管理をしています。Cargoは、コードのビルドやコードが依存しているライブラリのダウンロード、
それらのライブラリのビルド(コードが必要とするライブラリを我々は、*依存*と呼んでいます)などの多くの仕事を扱ってくれるからです。

<!--
The simplest Rust programs, like the one we’ve written so far, don’t have any
dependencies. So if we had built the Hello, world! project with Cargo, it would
only use the part of Cargo that handles building your code. As you write more
complex Rust programs, you’ll add dependencies, and if you start a project
using Cargo, adding dependencies will be much easier to do.
-->

今までに書いたような最も単純なRustプログラムは、依存がありません。従って、Hello, world!プロジェクトをCargoを使ってビルドしても、
Cargoのコードをビルドする部分しか使用しないでしょう。より複雑なRustプログラムを書くにつれて、
依存を追加し、Cargoでプロジェクトを開始したら、依存の追加は、遥かに簡単になるのです。

<!--
Because the vast majority of Rust projects use Cargo, the rest of this book
assumes that you’re using Cargo too. Cargo comes installed with Rust if you
used the official installers discussed in the “Installation” section. If you
installed Rust through some other means, check whether Cargo is installed by
entering the following into your terminal:
-->

Rustプロジェクトの大多数がCargoを使用しているので、これ以降この本では、あなたもCargoを使用していることを想定します。
Cargoは、「インストール」節で議論した公式のインストーラを使用していれば、勝手にインストールされます。
Rustを他の何らかの手段でインストールした場合、以下のコマンドを端末に入れてCargoがインストールされているか確かめてください:

```text
$ cargo --version
```

<!--
If you see a version number, you have it! If you see an error, such as `command
not found`, look at the documentation for your method of installation to
determine how to install Cargo separately.
-->

バージョンナンバーが見えたら、インストールされています！`command not found`などのエラーが見えたら、
自分のインストール方法をドキュメンテーションで確認して、Cargoを個別にインストールする方法を決定してください。

<!--
### Creating a Project with Cargo
-->

### Cargoでプロジェクトを作成する

<!--
Let’s create a new project using Cargo and look at how it differs from our
original Hello, world! project. Navigate back to your *projects* directory (or
wherever you decided to store your code). Then, on any operating system, run
the following:
-->

Cargoを使用して新しいプロジェクトを作成し、元のHello, world!プロジェクトとどう違うかを見ましょう。
*projects*ディレクトリ(あるいはコードを格納すると決めた場所)に戻ってください。それから、
OSに関わらず、以下を実行してください:

```text
$ cargo new hello_cargo --bin
$ cd hello_cargo
```

<!--
The first command creates a new binary executable called *hello_cargo*. The
`--bin` argument passed to `cargo new` makes an executable application (often
just called a *binary*) as opposed to a library. We’ve named our project
*hello_cargo*, and Cargo creates its files in a directory of the same name.
-->

最初のコマンドは、*hello_cargo*という新しいバイナリの実行可能ファイルを作成します。`cargo new`に渡した`--bin`引数が、
ライブラリとは対照的に実行可能なアプリケーション(よく単に*バイナリ*と呼ばれる)を作成します。プロジェクトを*hello_cargo*と名付け、
Cargoは、そのファイルを同名のディレクトリに作成します。

<!--
Go into the *hello_cargo* directory and list the files. You’ll see that Cargo
has generated two files and one directory for us: a *Cargo.toml* file and a
*src* directory with a *main.rs* file inside. It has also initialized a new Git
repository along with a *.gitignore* file.
-->

*hello_cargo*ディレクトリに行き、ファイルを列挙してください。Cargoが2つのファイルと1つのディレクトリを生成してくれたことがわかるでしょう:
*Cargo.toml*ファイルと、中に*main.rs*ファイルがある*src*ディレクトリです。また、
*.gitignore*ファイルと共に、新しいGitリポジトリも初期化しています。

<!--
> Note: Git is a common version control system. You can change `cargo new` to
> use a different version control system or no version control system by using
> the `--vcs` flag. Run `cargo new --help` to see the available options.
-->

> 注釈: Gitは一般的なバージョンコントロールシステムです。`cargo new`を変更して、異なるバージョンコントロールシステムを使用したり、
> `--vcs`フラグを使用して何もバージョンコントロールシステムを使用しないようにもできます。
> `cargo new --help`を走らせて、利用可能なオプションを確認してください。

<!--
Open *Cargo.toml* in your text editor of choice. It should look similar to the
code in Listing 1-2.
-->

お好きなテキストエディタで*Cargo.toml*を開いてください。リスト1-2のコードのような見た目のはずです。

<!--
<span class="filename">Filename: Cargo.toml</span>
-->

<span class="filename">ファイル名: Cargo.toml</span>

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2018"

[dependencies]
```

<!--
<span class="caption">Listing 1-2: Contents of *Cargo.toml* generated by `cargo
new`</span>
-->

<span class="caption">リスト1-2: `cargo new`で生成される*Cargo.toml*の中身</span>

<!--
This file is in the [*TOML*][toml] (*Tom’s Obvious, Minimal
Language*) format, which is Cargo’s configuration format.
-->

このファイルは[TOML][toml](*Tom's Obvious, Minimal Language*; `直訳`: トムの明確な最小限の言語)フォーマットで、
Cargoの設定フォーマットです。

[toml]: https://github.com/toml-lang/toml

<!--
The first line, `[package]`, is a section heading that indicates that the
following statements are configuring a package. As we add more information to
this file, we’ll add other sections.
-->

最初の行の`[package]`は、後の文がパッケージを設定していることを示すセクションヘッダーです。もっと情報を追加するにつれて、
別のセクションも追加するでしょう。

<!--
The next three lines set the configuration information Cargo needs to compile
your program: the name, the version, and the edition of Rust to use. We’ll talk
about the `edition` key in [Appendix E][appendix-e]<!-- ignore -->.
-->

その後の3行が、Cargoがプログラムをコンパイルするのに必要な設定情報をセットします: 名前、バージョン、使用するRustのエディションです。
`edition`キーについては、[Appendix E][appendix-e]<!-- ignore -->で話題にします。

<!--
The last line, `[dependencies]`, is the start of a section for you to list any
of your project’s dependencies. In Rust, packages of code are referred to as
*crates*. We won’t need any other crates for this project, but we will in the
first project in Chapter 2, so we’ll use this dependencies section then.
-->

最後の行の`[dependencies]`は、プロジェクトの依存を列挙するためのセクションの始まりです。
Rustでは、パッケージのコードは*クレート*として参照されます。このプロジェクトでは何も他のクレートは必要ありませんが、
第2章の最初のプロジェクトでは必要なので、その時にはこの依存セクションを使用するでしょう。

<!--
Now open *src/main.rs* and take a look:
-->

では、*src/main.rs*を開いて覗いてみてください:

<!--
<span class="filename">Filename: src/main.rs</span>
-->

<span class="filename">ファイル名: src/main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

<!--
Cargo has generated a Hello, world! program for you, just like the one we wrote
in Listing 1-1! So far, the differences between our previous project and the
project Cargo generates are that Cargo placed the code in the *src* directory,
and we have a *Cargo.toml* configuration file in the top directory.
-->

ちょうどリスト1-1で書いたように、CargoはHello, world!プログラムを生成してくれています。ここまでで、
前のプロジェクトとCargoが生成したプロジェクトの違いは、Cargoが*src*ディレクトリにコードを配置し、
最上位のディレクトリに*Cargo.toml*設定ファイルがあることです。

<!--
Cargo expects your source files to live inside the *src* directory. The
top-level project directory is just for README files, license information,
configuration files, and anything else not related to your code. Using Cargo
helps you organize your projects. There’s a place for everything, and
everything is in its place.
-->

Cargoは、ソースファイルが*src*ディレクトリにあることを期待します。プロジェクトの最上位のディレクトリは、
READMEファイル、ライセンス情報、設定ファイル、あるいは、他のコードに関連しないもののためのものです。
Cargoを使用すると、プロジェクトを体系化する手助けをしてくれます。適材適所であり、
全てがその場所にあるのです。

<!--
If you started a project that doesn’t use Cargo, as we did with the Hello,
world! project, you can convert it to a project that does use Cargo. Move the
project code into the *src* directory and create an appropriate *Cargo.toml*
file.
-->

Hello, world!プロジェクトのように、Cargoを使用しないプロジェクトを開始したら、
実際にCargoを使用するプロジェクトに変換することができます。プロジェクトのコードを*src*ディレクトリに移動し、
適切な*Cargo.toml*ファイルを作成してください。

<!--
### Building and Running a Cargo Project
-->

### Cargoプロジェクトをビルドし、実行する

<!--
Now let’s look at what's different when we build and run the Hello, world!
program with Cargo! From your *hello_cargo* directory, build your project by
entering the following command:
-->

さて、CargoでHello, world!プログラムをビルドし、実行する時の違いに目を向けましょう！*hello_cargo*ディレクトリから、
以下のコマンドを入力してプロジェクトをビルドしてください:

```text
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

<!--
This command creates an executable file in *target/debug/hello_cargo* (or
*target\debug\hello_cargo.exe* on Windows) rather than in your current
directory. You can run the executable with this command:
-->

このコマンドは、カレントディレクトリではなく、*target/debug/hello_cargo*(あるいはWindowsなら、
*target/debug/hello_cargo.exe*)に実行可能ファイルを作成します。以下のコマンドで実行可能ファイルを実行できます:

```text
$ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
                             # あるいは、Windowsなら、.\target\debug\hello_cargo.exe
Hello, world!
```

<!--
If all goes well, `Hello, world!` should print to the terminal. Running `cargo
build` for the first time also causes Cargo to create a new file at the top
level: *Cargo.lock*. This file keeps track of the exact versions of
dependencies in your project. This project doesn’t have dependencies, so the
file is a bit sparse. You won’t ever need to change this file manually; Cargo
manages its contents for you.
-->

全てがうまくいけば、`Hello, world!`が端末に出力されるはずです。初めて`cargo build`を実行すると、
Cargoが最上位に新しいファイルも作成します: *Cargo.lock*です。このファイルは、自分のプロジェクトの依存の正確なバージョンを追いかけます。
このプロジェクトには依存がないので、ファイルはやや空っぽです。絶対にこのファイルを手動で変更する必要はないでしょう;
Cargoが中身を管理してくれるのです。

<!--
We just built a project with `cargo build` and ran it with
`./target/debug/hello_cargo`, but we can also use `cargo run` to compile the
code and then run the resulting executable all in one command:
-->

`cargo build`でプロジェクトをビルドし、`./target/debug/hello_cargo`で実行したばかりですが、
`cargo run`を使用して、コードをコンパイルし、それから吐かれた実行可能ファイルを全部1コマンドで実行することもできます:

```text
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

<!--
Notice that this time we didn’t see output indicating that Cargo was compiling
`hello_cargo`. Cargo figured out that the files hadn’t changed, so it just ran
the binary. If you had modified your source code, Cargo would have rebuilt the
project before running it, and you would have seen this output:
-->

今回は、Cargoが`hello_cargo`をコンパイルしていることを示唆する出力がないことに注目してください。
Cargoはファイルが変更されていないことを推察したので、単純にバイナリを実行したのです。
ソースコードを変更していたら、Cargoは実行前にプロジェクトを再ビルドし、こんな出力を目の当たりにしたでしょう:

```text
$ cargo run
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

<!--
Cargo also provides a command called `cargo check`. This command quickly checks
your code to make sure it compiles but doesn’t produce an executable:
-->

Cargoは`cargo check`というコマンドも提供しています。このコマンドは、迅速にコードを確認し、
コンパイルできることを確かめますが、実行可能ファイルは生成しません:

```text
$ cargo check
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

<!--
Why would you not want an executable? Often, `cargo check` is much faster than
`cargo build`, because it skips the step of producing an executable. If you’re
continually checking your work while writing the code, using `cargo check` will
speed up the process! As such, many Rustaceans run `cargo check` periodically
as they write their program to make sure it compiles. Then they run `cargo
build` when they’re ready to use the executable.
-->

何故、実行可能ファイルが欲しくないのでしょうか？しばしば、`cargo check`は、`cargo build`よりも遥かに速くなります。
実行可能ファイルを生成する手順を飛ばすからです。コードを書いている際に継続的に自分の作業を確認するのなら、
`cargo check`を使用すると、その過程が高速化されます！そのため、多くのRustaceanは、
プログラムを書く際にコンパイルできるか確かめるために定期的に`cargo check`を実行します。
そして、実行可能ファイルを使用できる状態になったら、`cargo build`を走らせるのです。

<!--
Let’s recap what we’ve learned so far about Cargo:
-->

ここまでにCargoについて学んだことをおさらいしましょう:

<!--
* We can build a project using `cargo build` or `cargo check`.
* We can build and run a project in one step using `cargo run`.
* Instead of saving the result of the build in the same directory as our code,
Cargo stores it in the *target/debug* directory.
-->

* `cargo build`か`cargo check`でプロジェクトをビルドできる。
* プロジェクトのビルドと実行を1ステップ、`cargo run`でできる。
* ビルドの結果をコードと同じディレクトリに保存するのではなく、Cargoは*target/debug*ディレクトリに格納する。

<!--
An additional advantage of using Cargo is that the commands are the same no
matter which operating system you’re working on. So, at this point, we’ll no
longer provide specific instructions for Linux and macOS versus Windows.
-->

Cargoを使用する追加の利点は、使用しているOSに関わらず、同じコマンドが使用できることです。
故にこの時点で、WindowsとLinux及びmacOSで特定の手順を提供することは最早なくなります。

<!--
### Building for Release
-->

### リリースビルドを行う

<!--
When your project is finally ready for release, you can use `cargo build
--release` to compile it with optimizations. This command will create an
executable in *target/release* instead of *target/debug*. The optimizations
make your Rust code run faster, but turning them on lengthens the time it takes
for your program to compile. This is why there are two different profiles: one
for development, when you want to rebuild quickly and often, and another for
building the final program you’ll give to a user that won’t be rebuilt
repeatedly and that will run as fast as possible. If you’re benchmarking your
code’s running time, be sure to run `cargo build --release` and benchmark with
the executable in *target/release*.
-->

プロジェクトを最終的にリリースする準備ができたら、`cargo build --release`を使用して、
最適化を行なってコンパイルすることができます。このコマンドは、*target/debug*ではなく、
*target/release*に実行可能ファイルを作成します。最適化は、Rustコードの実行を速くしてくれますが、
オンにするとプログラムをコンパイルする時間が延びます。このため、2つの異なるプロファイルがあるのです:
頻繁に再ビルドをかけたい開発用と、繰り返し再ビルドすることはなく、できるだけ高速に動いてユーザにあげる最終的なプログラムをビルドする用です。
コードの実行時間をベンチマークするなら、`cargo build --release`を確実に実行し、*target/release*の実行可能ファイルでベンチマークしてください。

<!--
### Cargo as Convention
-->

### 習慣としてのCargo

<!--
With simple projects, Cargo doesn’t provide a lot of value over just using
`rustc`, but it will prove its worth as your programs become more intricate.
With complex projects composed of multiple crates, it’s much easier to let
Cargo coordinate the build.
-->

単純なプロジェクトでは、Cargoは単に`rustc`を使用する以上の価値を生みませんが、プログラムが複雑になるにつれて、
その価値を証明するでしょう。複数のクレートからなる複雑なプロジェクトでは、Cargoにビルドを調整してもらうのが遥かに簡単です。

<!--
Even though the `hello_cargo` project is simple, it now uses much of the real
tooling you’ll use in the rest of your Rust career. In fact, to work on any
existing projects, you can use the following commands to check out the code
using Git, change to that project’s directory, and build:
-->

`hello_cargo`プロジェクトは単純ではありますが、今では、Rustのキャリアを通じて使用するであろう本物のツールを多く使用するようになりました。
事実、既存のどんなプロジェクトに取り組むにも、以下のコマンドを使用して、Gitでコードをチェックアウトし、
そのプロジェクトのディレクトリに移動し、ビルドできます:

```text
$ git clone someurl.com/someproject
$ cd someproject
$ cargo build
```

<!--
For more information about Cargo, check out [its documentation].
-->

Cargoについてより詳しく知るには、[ドキュメンテーション]を確認してください。

[ドキュメンテーション]: https://doc.rust-lang.org/cargo/

<!--
## Summary
-->

## まとめ

<!--
You’re already off to a great start on your Rust journey! In this chapter,
you’ve learned how to:
-->

既にRustの旅の素晴らしいスタートを切っています！この章では、以下の方法を学びました:

<!--
* Install the latest stable version of Rust using `rustup`
* Update to a newer Rust version
* Open locally installed documentation
* Write and run a Hello, world! program using `rustc` directly
* Create and run a new project using the conventions of Cargo
-->

* `rustup`で最新の安定版のRustをインストールする方法
* 新しいRustのバージョンに更新する方法
* ローカルにインストールされたドキュメンテーションを開く方法
* 直接`rustc`を使用してHello, world!プログラムを書き、実行する方法
* Cargoの慣習を使用して新しいプロジェクトを作成し、実行する方法

<!--
This is a great time to build a more substantial program to get used to reading
and writing Rust code. So, in Chapter 2, we’ll build a guessing game program.
If you would rather start by learning how common programming concepts work in
Rust, see Chapter 3 and then return to Chapter 2.
-->

より中身のあるプログラムをビルドし、Rustコードの読み書きに慣れるいいタイミングです。故に、第2章では、
数当てゲームを構築します。むしろ一般的なプログラミングの概念がRustでどう動くのか学ぶことから始めたいのであれば、
第3章を見て、それから第2章に戻ってください。
