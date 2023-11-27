# End-to-End Encryption (E2EE) Protocol for Universal Profiles

This protocol establishes secure communication between two Universal Profiles on LUKSO, ensuring that only the sender and the intended recipient can decrypt the messages exchanged between them.

## Key Exchange

The first step in the E2EE protocol is the exchange of encryption keys between the two profiles. This is done using The Double Ratchet Algorithm, a key management algorithm that provides forward secrecy and cryptographic deniability. The Double Ratchet Algorithm is used by the Signal messaging app and is described in detail in the [Signal Protocol Documentation](https://signal.org/docs/specifications/doubleratchet/).

A profile broadcasts an identity and an ephemeral public key to the network. The identity key is a long-term key used to identify the profile, while the ephemeral key is a short-term key used to establish a shared secret key with another profile. The ephemeral key is rotated periodically to ensure forward secrecy.

When a profile wants to send a message to another profile, it first retrieves the ephemeral public key of the recipient from the network. It then uses the Double Ratchet Algorithm to establish a shared secret key with the recipient, which is used to encrypt the message.

## Message Ordering

To ensure that messages are received in the correct order, each message is also assigned a sequence number. The sequence number is incremented by one for each message and sent with the encrypted message.

## Message Encryption

Once the shared secret key has been established, both profiles can establish a root key and a chain key. The root key is used to derive a new chain key for each message, which is used to encrypt the message. The chain key is then updated to derive a new chain key for the next message. The message is encrypted using the AES-256-CBC algorithm with a random initialization vector (IV) and a random padding. The encrypted message is then sent to the recipient.

## Message Authentication

To ensure that messages have not been tampered with during transmission, each message is also authenticated using the HMAC-SHA256 algorithm. This algorithm generates a unique message authentication code (MAC) for each message, which is sent along with the encrypted message.

## Message History

To ensure that messages are not lost, each profile stores a history of all messages that have been sent and received. This history is stored in a local database, and is used to retrieve messages later on.

It is important to note that message history is not stored on the blockchain but rather in a local database. This means that there is only one copy of the message history, which is stored on the profile owner's device. This ensures that messages cannot be deleted or modified by anyone other than the profile owner.

## Conclusion

By using the E2EE protocol, Lukso profiles can communicate securely and privately without the risk of eavesdropping or message tampering.
