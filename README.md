# payInETH

## Setup

* Reference - https://docs.scrt.network/secret-network-documentation/development/readme-1
  * Install Git and Make - https://docs.scrt.network/secret-network-documentation/development/readme-1/setting-up-your-environment#install-requirements

  * Install Rust
    ```
    rustup toolchain use stable
    rustup target add wasm32-unknown-unknown
    source "$HOME/.cargo/env"
    ```
  * Install Cargo Generate
    ```
    cargo install cargo-generate --features vendored-openssl
    ```
  * SKIP Install Secret CLI - https://github.com/scrtlabs/SecretNetwork/releases/latest/download/secretcli-MacOS-arm64
    * Note: SKIP since commits not with GPG keys, use secretjs instead
  * Run LocalSecret on Linode
    ```
    ssh root@xx.xx.xx.xx

    docker run -it -p 9091:9091 -p 26657:26657 -p 1317:1317 -p 5000:5000 \
      --name localsecret ghcr.io/scrtlabs/localsecret:latest
    ```
    * Other
      ```
      docker logs -f localsecret

      docker restart localsecret

      docker stop localsecret && docker rm localsecret
      ```

  * Install dependencies
    ```
    npm install --global lerna
    yarn set version 4.2.2
    corepack enable
    corepack prepare yarn@v4.2.2 --activate
    ```

### Projects

#### Upload Contract

```bash
cd packages/uploadContract
```

* Install SecretJS
  ```
  yarn add secretjs
  ```

Run the commands mentioned in the specific project [README](./packages/uploadContract/README.md]

#### Instantiate Contract

```bash
cd packages/instantiateContract
```

Run the commands mentioned in the specific project [README](./packages/instantiateContract/README.md]

#### Compile and Deploy Contract (Example: Counter)

https://docs.scrt.network/secret-network-documentation/development/readme-1/compile-and-deploy

```
mkdir -p contract && cd contract
cargo generate --git https://github.com/scrtlabs/secret-template.git --name my-counter-contract
```

* Compile. Note: Outputs contract.wasm and contract.wasm.gz file in the root directory of the contract folder

```
cd contract/my-counter-contract
make build
```

* TODO - optimize contract code


