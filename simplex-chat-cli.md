# How to install Simplex Chat CLI on Mac M1

You should be able to install SimpleX Chat CLI by following the steps.

1. Install [Haskell GHCup](https://www.haskell.org/ghcup/), GHC 8.10.7 and cabal:
2. Build the project by the following commands:

```
git clone git@github.com:simplex-chat/simplex-chat.git
```

```
cd simplex-chat
```

```
git checkout stable
```

Verify what version of openssl you have installed by running:

```
brew search openssl
```

You should see something like the following

```
==> Formulae
glib-openssl    openssl@1.1 ✔   openssl@3 ✔     openssl@3.0     openslp         openssh         opensaml        opensc          open-sp         openfst         opencsg         openmsx

==> Casks
openmsx                                                            opensc                                                             opensim
```

If you didn't installed openssl yet or you have installed only openssl@1.1 I suggest to install openssl 3 via homebrew as follows:

```
brew install openssl@3
```

You should previously also check whether you have installed llvm and what version; you can proceed via Homebrew by checking as follows


```
brew search llvm
```
You should see something like the following

```
==> Formulae
cargo-llvm-lines                 llvm@11                          llvm@13 ✔                        llvm@15                          llvm@8                           spirv-llvm-translator
llvm ✔                           llvm@12                          llvm@14                          llvm@7                           llvm@9                           wllvm
```

If you didn't installed llvm yet or you have installed only llvm@13, I suggest to install llvm@13 via homebrew as follows:

```
brew install llvm@13
```

Be careful after the installation to add the PATH to the file `.zshrc`.

Open `.zshrc` and control that the line was correctly added.
Rember that if you modify the file, after exiting from the editor, it's necessary to run `source .zshrc`.

Then, be sure to stay under the folder `simplex-chat` and run

```
cp scripts/cabal.project.local.mac cabal.project.local
```

Open cabal.project.local to make some changes, and precisely be sure that in the following lines there is openssl@3 as follows:

```
 extra-include-dirs: /opt/homebrew/opt/openssl@3/include
    extra-lib-dirs: /opt/homebrew/opt/openssl@3/lib
```

Check the correct path of the file cabal.project under the folder simplex-chat, and then open the file `Controller.hs` which is under `simplex-chat/src/Simplex/Chat/`. You can jump directly to the line that should be modified by running:

```
nano +77 Controller.hs
```

Modify the PATH that is after `B.readFile` with the correct one where is the file `cabal.project`; it should be something like `/Users/foo/simplex-chat/cabal.project`.

In the end run:

```
cabal update
```

and then

```
cabal install
```

If all is correct you will have simplex-chat compiled and installed on your Mac M1 and you can use it by simply running 

```
simplex-chat
```

That's all.