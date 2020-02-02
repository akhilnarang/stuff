# IS

## Chapter 3

### Key Management

#### Techniques

- Symmetric Key Encryption
- Public Key Encryption

#### Symmetric Key Encryption Techniques

- Physical delivery between the two parties.
- A third party can select and physically deliver.
- If a key has been previously used by the two parties, encrypt new key using old key.
- If both parties have an encrypted connection with a mutual third party, it can deliver the key.

Session keys are temporary keys that are generated at the start of every new session.
Communication between end systems is encrypted using this.

For each end system or user there is a unique master key that it shares with the key distribution center. These master keys.

### Diffie-Hellman

In a Diffie-Hellman Key Exchange, Alice and Bob have chosen prime value = 17 and primitive root = 5. If Alice's secret key is 4 and Bob's secret key is 6, what is the secret key they exchanged?

Steps

- Both calculate the value of their public key

## Chapter 4

### Some topic

#### Network Based IDS

- It looks for attack signatures in network traffic.
- Filter is applied to determine which traffic will be discarded or passed onto an attack recognition module.
- Monitor, capture, and analyze.
- Detect malicious data present into packet.
- Analsyis - matches traffic to the library of known attack.

#### Limitations

- Analysis is very difficult in a busy network.

#### SSL Architecture

- SSL handshake protocol
- SSL Change cipher spec protocol
- SSL alert protocol
- HTTP

### Something else

#### Consider one way authentication

- A -> B : ID<sub>A</sub>
- B -> A : R<sub>n</sub>
- A -> B : E (PR<sub>a</sub>, R<sub>1</sub>)
- Explain protocol
- What type of attack is this susceptible to?

One way authentication scheme with 3 messages.

#### Another question

Users A and B use Diffie-Hellman key exchange with a common prime q = 71 , primitive root is 7. If user A has private key as 5, and user B has private key 12, what is the public key of of both? Find out shared secret key
