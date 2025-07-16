# QuantumVault: Secure and Verifiable Computation for Decentralized Identity

QuantumVault provides a Rust-based zk-SNARK circuit compiler and secure enclave runtime environment, enabling decentralized identity attestation and verifiable computation of aggregated on-chain data. This project aims to bridge the gap between sensitive user data and the transparency requirements of blockchain applications by enabling computation on encrypted data while proving the correctness of the computation without revealing the underlying information. QuantumVault enables privacy-preserving data aggregation and verifiable computation within decentralized ecosystems, making it suitable for applications like anonymous voting, secure data marketplaces, and private DeFi protocols.

At its core, QuantumVault provides a high-level domain-specific language (DSL) for defining zk-SNARK circuits. This DSL, built on top of Rust, allows developers to describe complex computations in a more intuitive manner compared to directly manipulating constraint systems. The compiler then translates this DSL into efficient R1CS representations suitable for generating zk-SNARK proofs. These proofs can be verified on-chain, guaranteeing the integrity of the computation. Furthermore, QuantumVault incorporates a secure enclave runtime environment, leveraging Intel SGX or similar technologies, to protect the sensitive data used in the computations. This ensures that even the node executing the computation cannot access or tamper with the user's private information.

The primary benefit of QuantumVault is its ability to unlock new possibilities for decentralized applications that require both privacy and verifiability. By enabling verifiable computation on encrypted data, QuantumVault empowers users to maintain control over their personal information while still participating in decentralized ecosystems. This addresses a critical challenge in the adoption of blockchain technology, where data privacy concerns often limit the scope of potential applications. Moreover, the Rust-based architecture provides excellent performance and security, making QuantumVault suitable for production environments. By combining a user-friendly circuit compiler with a secure enclave runtime, QuantumVault empowers developers to build privacy-preserving applications with confidence.

## Key Features

*   **Domain-Specific Language (DSL) for Circuit Definition:** QuantumVault includes a custom DSL for defining zk-SNARK circuits, simplifying the process of creating complex computations. The DSL supports arithmetic operations, conditional statements, and custom data structures. It generates an intermediate representation, which is then optimized and compiled into an R1CS constraint system. This abstraction layer simplifies circuit design, reduces errors, and improves developer productivity.

*   **Rust-based zk-SNARK Compiler:** The compiler translates the DSL code into an R1CS representation suitable for proof generation. The compiler leverages Rust's strong typing and memory safety guarantees to ensure the integrity of the compiled circuits. Supports multiple zk-SNARK proving systems (e.g., Groth16, Plonk) through a modular backend architecture.

*   **Secure Enclave Runtime (Intel SGX):** QuantumVault leverages Intel SGX (or similar secure enclave technologies like AMD SEV) to protect sensitive data and code execution within a hardened environment. This ensures that even if the host system is compromised, the data and computation remain secure. The runtime provides APIs for secure data storage, key management, and remote attestation.

*   **On-Chain Verification Support:** Generated zk-SNARK proofs can be verified on-chain using smart contracts. The project provides pre-built smart contract libraries for verifying Groth16 and Plonk proofs on various blockchains (e.g., Ethereum, Solana). This enables decentralized verification of the computations performed within the secure enclave.

*   **Data Aggregation Capabilities:** QuantumVault supports the aggregation of data from multiple sources while preserving privacy. The circuit compiler enables the definition of aggregation logic that operates on encrypted data within the secure enclave. This allows for secure and verifiable computation of statistics, averages, and other aggregated metrics.

*   **API for Data Injection and Extraction:** Secure APIs are provided for injecting encrypted data into the secure enclave and extracting verifiable computation results. These APIs ensure that data is properly encrypted and authenticated before being processed by the circuit.

*   **Remote Attestation:** The secure enclave runtime supports remote attestation, allowing external parties to verify the integrity of the enclave and the code running within it. This provides assurance that the computation is being performed in a trusted environment.

## Technology Stack

*   **Rust:** The primary programming language used for the circuit compiler, secure enclave runtime, and supporting libraries. Rust's memory safety and performance characteristics make it ideal for building secure and efficient cryptographic applications.
*   **zk-SNARKs (Groth16, Plonk):** Zero-knowledge Succinct Non-Interactive Arguments of Knowledge are used to generate proofs of computation correctness. The compiler supports multiple zk-SNARK proving systems, allowing developers to choose the best option for their specific use case.
*   **Intel SGX (or AMD SEV):** Secure enclave technology used to create a trusted execution environment for protecting sensitive data and code. SGX isolates the enclave from the rest of the system, preventing unauthorized access and tampering.
*   **WebAssembly (Wasm):** Circuits can be compiled to Wasm for portability and execution in different environments, including browsers and other resource-constrained devices.
*   **Ethereum (or Solana):** Smart contract platforms used for on-chain verification of zk-SNARK proofs. Pre-built smart contract libraries are provided for verifying proofs on these platforms.

## Installation

1.  **Install Rust:** If you don't have Rust installed, download and install it from [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install). Follow the instructions for your operating system. Ensure you have cargo installed and updated.

2.  **Clone the Repository:** Clone the QuantumVault repository from GitHub:
    `git clone https://github.com/jjfhwang/QuantumVault.git`
    `cd QuantumVault`

3.  **Install Dependencies:** Install the necessary dependencies using cargo:
    `cargo build --release`

4.  **Install Intel SGX SDK (Optional):** If you plan to use the secure enclave runtime, you need to install the Intel SGX SDK. Follow the instructions provided by Intel: [https://software.intel.com/en-us/sgx-sdk](https://software.intel.com/en-us/sgx-sdk) Make sure your CPU supports SGX and that SGX is enabled in your BIOS. If using AMD SEV, consult AMD's documentation for setup.

5.  **Build the Enclave (Optional):** Build the secure enclave component. This requires the SGX SDK to be properly installed and configured:
    `cd enclave`
    `make`

## Configuration

The QuantumVault project utilizes environment variables for configuration. Here are the key environment variables:

*   `QUANTUMVAULT_SGX_MODE`: (Optional) Specifies the SGX mode. Possible values: `Hardware` (requires SGX-enabled hardware), `Simulation` (for testing without SGX hardware). Default: `Simulation`.
*   `QUANTUMVAULT_PROOF_SYSTEM`: Specifies the zk-SNARK proving system to use. Possible values: `Groth16`, `Plonk`. Default: `Groth16`.
*   `QUANTUMVAULT_ENCLAVE_PATH`: (Optional) Specifies the path to the compiled secure enclave library (.so file). Required if using SGX. Default: `./enclave/enclave.signed.so`.

Example setting an environment variable (Linux/macOS):
`export QUANTUMVAULT_PROOF_SYSTEM=Plonk`

## Usage

The QuantumVault project consists of a circuit compiler and a secure enclave runtime.

**1. Circuit Compilation:**

Create a circuit definition file (e.g., `my_circuit.vault`). This file will contain the DSL code describing your zk-SNARK circuit.

Example DSL code:


Compile the circuit using the `quantumvaultc` compiler:
`cargo run --release --bin quantumvaultc my_circuit.vault -o my_circuit.r1cs`

This will generate the R1CS representation of the circuit (`my_circuit.r1cs`).

**2. Secure Enclave Runtime:**

To use the secure enclave runtime, you need to generate a zk-SNARK proof within the enclave. This involves loading the R1CS file into the enclave, providing input data, and generating the proof.

Example Rust code to interact with the enclave:


## Contributing

We welcome contributions to the QuantumVault project! Please follow these guidelines:

1.  Fork the repository and create a new branch for your feature or bug fix.
2.  Follow the Rust coding style and best practices.
3.  Write unit tests for your code.
4.  Submit a pull request with a clear description of your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/jjfhwang/QuantumVault/blob/main/LICENSE) file for details.

## Acknowledgements

We would like