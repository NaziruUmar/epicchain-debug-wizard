# EpicChain Smart Contract Debugger `launch.config` Reference

> **Note:** This document is specifically tailored for configuring EpicChain smart contracts using `.EVM` files. For details on EpicChain N3 smart contract configurations, please refer to [this document](debug-config-reference.md).

The EpicChain Smart Contract Debugger provides advanced execution control through detailed configuration settings specified in the `launch.json` file. This guide aims to elucidate each setting and its application to facilitate a seamless debugging experience.

## `program`

The `program` field specifies the absolute path to the `.EVM` (Epic Virtual Machine) file you wish to debug. This file represents the compiled smart contract and is crucial for the debugger to locate and execute the contract correctly.

**Example Configuration:**

```json
"program": "${workspaceFolder}/bin/Debug/netstandard2.0/publish/domain.evm"
```

- **`${workspaceFolder}`**: A placeholder for the root directory of your workspace, ensuring paths are resolved relative to this base directory.
- **`/bin/Debug/netstandard2.0/publish/domain.evm`**: The relative path pointing to the compiled `.EVM` file within your workspace.

**JSON Schema:**

```json
"program": {
    "type": "string"
}
```

**Explanation:** This setting must be a string that indicates the file path of the `.EVM` file. It can be either an absolute path or a relative path from the workspace root.

## `args`

The `args` field defines the command-line arguments to be passed to the smart contract's entry point. These arguments are essential for invoking specific methods or functionalities within the contract.

- **Hex-encoded byte arrays:** Strings starting with `0x` are interpreted as hexadecimal byte arrays.
- **Base-58 encoded addresses:** Strings beginning with `@` are considered as base-58 encoded addresses.

**Examples:**

```json
"args": ["register", ["epic.org", "Alice Smith"]],

"args": ["getTransactionDetails", ["0x4a3c9e07b1f56f07ab329b6e38c6b0d4f1b2b7c5f3f6d7b90c5d12a3efcd6a1b"]],

"args": ["balanceOf", ["@6hT1t9zLJn9kR8VpM7J8uJ3K7tP2L9P4bM"]],
```

**JSON Schema:**

```json
"args": {
    "type": "array",
    "default": []
}
```

**Explanation:** The `args` setting is an array of strings representing command-line arguments. Each argument can be a plain string, a hex-encoded byte array, or a base-58 encoded address.

## `return-types`

The `return-types` setting specifies the expected return type of the smart contract’s entry point. This is particularly useful for contracts that return a strongly-typed value rather than a generic `object`.

**Note:** EpicChain smart contracts might return multiple values, but for simplicity, the `return-types` property is specified as an array even if there’s only one return value.

**Examples:**

```json
"return-types": ["bool"],

"return-types": ["string"],
```

**JSON Schema:**

```json
"return-types": {
    "type": "array",
    "items": {
        "type": "string",
        "enum": [
            "int",
            "bool",
            "string",
            "hex",
            "byte[]"
        ]
    }
}
```

**Explanation:** This setting is an array of strings where each string represents a return type. Supported types include `int`, `bool`, `string`, `hex`, and `byte[]`.

## `checkpoint`

The `checkpoint` field specifies the path to an EpicChain checkpoint file used for blockchain data. This setting is essential for initializing the blockchain state to a specific point in time during debugging.

**Example Configuration:**

```json
"checkpoint": "${workspaceFolder}/checkpoints/3-mint-tokens-invoked.epicchain-checkpoint"
```

**JSON Schema:**

```json
"checkpoint": {
    "type": "string"
}
```

**Explanation:** This setting should be a string representing the path to the EpicChain checkpoint file, either absolute or relative to the workspace root.

## `storage`

The `storage` field is used to populate the debugger’s emulated storage with key/value pairs. This allows for simulating specific storage states during debugging. Hex-encoded byte arrays are used for values when necessary.

**Examples:**

```json
"storage": [
    {
        "key": "epic.org",
        "value": "Epic Foundation"
    }
],

"storage": [
    {
        "key": "0x8a6f1e4f13022b26e56e957cb8251b082f0748b1007465737361",
        "value": "0x174876e800"
    },
    {
        "key": "0x796c707075536c61746f740074636172746e6f63",
        "value": "0x174876e800"
    }
]
```

**JSON Schema:**

```json
"storage": {
    "type": "array",
    "items": {
        "type": "object",
        "required": [
            "key",
            "value"
        ],
        "properties": {
            "key": {
                "type": "string"
            },
            "value": {
                "type": "string"
            },
            "constant": {
                "type": "boolean"
            }
        }
    },
    "default": []
}
```

**Explanation:** This setting is an array of objects where each object contains a `key` and `value` for storage simulation. The `key` can be a plain string or a hex-encoded string, and the `value` can be a string or a hex-encoded string.

## `sourceFileMap`

The `sourceFileMap` setting is used for mapping source file paths to their locations in the debugger. This is optional but useful for debugging if the source files are located in different directories.

**Example Configuration:**

```json
"sourceFileMap": {
    "C:\\projects\\epicchain": "/home/user/epicchain"
}
```

**JSON Schema:**

```json
"sourceFileMap": {
    "type": "object",
    "additionalProperties": {
        "type": "string"
    }
}
```

**Explanation:** This setting is an object where keys are source file paths on the local machine, and values are their corresponding paths in the debugger environment.

## `stored-contracts`

The `stored-contracts` field allows for additional contracts to be loaded for dynamic invocation scenarios. These contracts can also include optional emulated storage key/value pairs.

**Example Configuration:**

```json
"stored-contracts": [
    "${workspaceFolder}/Second/bin/Debug/netstandard2.0/Second.evm",
    {
        "program": "${workspaceFolder}/Third/bin/Debug/netstandard2.0/Third.evm",
        "storage": [
            {
                "key": "epic.org",
                "value": "Epic Foundation"
            }
        ]
    }
]
```

**JSON Schema:**

```json
"stored-contracts": {
    "type": "array",
    "items": {
        "oneOf": [
            {
                "type": "string",
                "description": "Absolute path to EVM file"
            },
            {
                "type": "object",
                "required": [
                    "program"
                ],
                "properties": {
                    "program": {
                        "type": "string"
                    },
                    "storage": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "required": [
                                "key",
                                "value"
                            ],
                            "properties": {
                                "key": {
                                    "type": "string"
                                },
                                "value": {
                                    "type": "string"
                                },
                                "constant": {
                                    "type": "boolean"
                                }
                            }
                        }
                    }
                }
            }
        ]
    }
}
```

**Explanation:** This setting is an array where each item can either be a string specifying the path to an `.EVM` file or an object with `program` and optional `storage` properties. 

## `runtime`

The `runtime` setting determines the behavior of `Runtime.Trigger` and `Runtime.CheckWitness` methods within the smart contract.

- **`Runtime.Trigger`** can return either `TriggerType.Verification` or `TriggerType.Application`. By default, it returns `TriggerType.Application`, but this can be overridden using the `runtime.trigger` configuration.
- **`Runtime.CheckWitness`** can be configured to return a fixed boolean result or compare against a list of hex-encoded byte arrays.

**Examples:**

```json
"runtime": {
    "trigger": "verification",
    "witnesses": {
        "check-result": true
    }
}
```

**JSON Schema:**

```json
"runtime": {
    "type": "object",
    "properties": {
        "trigger": {
            "type": "string",
            "enum": [
                "verification",
                "application"
            ]
        },
        "witnesses": {
            "oneOf": [
                {
                    "type": "array",
                    "items": "string"
                },
                {
                    "type":

```json
                    "object",
                    "required": [
                        "check-result"
                    ],
                    "properties": {
                        "check-result": {
                            "type": "boolean"
                        }
                    }
                }
            ]
        }
    }
}
```

**Explanation:** 
- The `trigger` property determines the type of trigger for `Runtime.Trigger`, which can be `verification` or `application`.
- The `witnesses` property can either be an array of hex-encoded byte arrays (representing valid witness values) or an object with a `check-result` property that specifies a fixed boolean result for `Runtime.CheckWitness`.

## `utxo`

The `utxo` field specifies the UTXO (Unspent Transaction Outputs) assets, such as EpicChain and EpicPulse, to attach to the transaction being debugged. This setting helps simulate transactions by providing the necessary inputs and outputs for the contract's execution.

**Example Configuration:**

```json
"utxo": {
    "inputs": [
        {
            "txid": "0xf5e388f6a98a133755190f06e4dd3c9d9afd916a1e27b52250f1d54d405086cf",
            "n": 0
        }
    ],
    "outputs": [
        {
            "asset": "epicchain",
            "value": 1000,
            "address": "0x30f41a14ca6019038b055b585d002b287b5fdd47"
        }
    ]
}
```

**JSON Schema:**

```json
"utxo": {
    "type": "object",
    "properties": {
        "inputs": {
            "type": "array",
            "items": {
                "type": "object",
                "required": [
                    "txid",
                    "n"
                ],
                "properties": {
                    "txid": { "type": "string" },
                    "n": { "type": "number" },
                    "value": { "type": "number" }
                }
            }
        },
        "outputs": {
            "type": "array",
            "items": {
                "type": "object",
                "required": [
                    "asset",
                    "value",
                    "address"
                ],
                "properties": {
                    "asset": { "type": "string" },
                    "value": { "type": "number" },
                    "address": { "type": "string" }
                }
            }
        }
    }
}
```

**Explanation:** 
- **`inputs`**: An array specifying the UTXO inputs for the transaction. Each input includes a `txid` (transaction ID), `n` (index of the output in the transaction), and an optional `value`.
- **`outputs`**: An array specifying the UTXO outputs for the transaction. Each output includes an `asset` (such as `epicchain` or `epicpulse`), a `value` (amount of the asset), and an `address` (destination address).
