# Teaching patterns and behavioral checks

Use these examples to recognize structure, not to recite fixed wording or teach networking by default. Match the learner's language and established knowledge.

## 1. Motivate before naming

Learner: “How does the sender know whether the receiver got the data?”

An unexplained jump:

> TCP uses ACKs, cumulative acknowledgement, sequence numbers, RTO, SACK, and retransmission queues.

A focused next step:

> After sending, the sender can observe its own send operation but cannot directly observe the receiver's memory. The receiver can therefore send a reply confirming what it received. That reply is an acknowledgement, abbreviated ACK. In TCP, it confirms received bytes; it does not say that an application saved a chat message. If the reply never arrives, the sender still does not know whether the data or the reply was lost. That is the next problem to solve.

This introduces one mechanism, establishes its need, and leaves the next failure as the bridge. Do not immediately append the complete retry, deduplication, routing, and encryption lesson unless requested.

## 2. Repair an unexplained qualifier

Learner: “Why did you suddenly say 'ordinary copy send path'?”

Do not respond by cataloguing every zero-copy API.

Repair:

> The missing point is where the bytes remain while sending is still in progress. The application originally owns the memory containing them. In the implementation branch being discussed, the operating system copies those bytes into memory it manages, so later transmission can use that data. “Copy” names that action. There was no need to introduce the broader label before explaining the action.

When subsequently examining source, explain that this is the selected branch. Do not turn the narrowed example into “all systems always copy every byte.”

## 3. Keep code actors separate

Confusing convenience helper:

```python
def connect(listener):
    return socket.create_connection(listener.getsockname())
```

The learner may infer that a remote client can access the server's listening object.

When addresses and sockets have already been introduced, prefer:

```python
server_address = ("127.0.0.1", 18765)
client_connection = socket.create_connection(server_address)
```

Explain that the address is configuration known to the client and that the client creates its own connection object. If a same-process helper is useful, explicitly describe it as local test wiring; no object is transmitted to the remote client.

Do not use this example before introducing the meaning of the address and port if those are unknown to the learner.

## 4. Introduce only code needed by the current question

Current question: “Why does the receiver need to know the encoding?”

Before running, explain that the command converts one character to bytes and decodes the same bytes using two rules. It makes no network request and writes no file.

```bash
python3 - <<'PY'
data = "é".encode("utf-8")
print("bytes:", list(data))
print("UTF-8:", data.decode("utf-8"))
print("Latin-1:", data.decode("latin-1"))
PY
```

Explain before or alongside the example: an encoding is a rule relating text to bytes; UTF-8 and Latin-1 are different rules. The middle shell lines are Python code passed to Python through its standard input; do not make the shell wrapper a separate lesson unless needed.

Expected output:

```text
bytes: [195, 169]
UTF-8: é
Latin-1: Ã©
```

Interpretation: the bytes were unchanged, yet different decoding rules produced different text. Agreeing on how to interpret bytes is distinct from transferring them intact. This example does not demonstrate any actual transmission.

The lesson should not detour into sockets or Unicode normalization unless the learner asks or the next question requires it.

## 5. Read implementation after establishing the question

Learner: “Can you show how this is done in the kernel?”

Use this sequence:

1. Identify the mechanism currently being explained, such as accepting bytes from an application or processing an acknowledgement.
2. State the exact kernel and revision being inspected; verify the relevant source.
3. Explain the role of the few structures or fields required by that excerpt.
4. Show a short excerpt with its source link and applicable branch context.
5. Explain the state before, the operation performed, and the state afterward.
6. Explain what the return value or trace actually establishes.

Do not quote an entire function just to prove it was found. Do not claim a macOS command executed Linux source. If only a simplified model is available, call it a model and distinguish which pieces use real packet formats or real sockets.

## 6. Respect continuation and scope

Conversation state: the learner understands bytes, a local socket, and an IP address. The outstanding question is how traffic arriving at a machine reaches the intended service.

For “continue,” or its equivalent in the learner's language, motivate service selection on the same machine before introducing a port. Do not re-teach UTF-8, jump to congestion control, or demand a quiz answer before continuing.

For “Give the whole explanation in one answer,” expand the number of causal steps while preserving dependency order. “One by one” must not become a reason to leave a requested complete tutorial unfinished.

## 7. Transfer the method beyond networking

Learner: “Teach database transactions from scratch.”

Start with a concrete operation that changes two records and the problem if only the first change completes. Motivate grouping related changes before naming a transaction. Do not open with ACID, isolation levels, write-ahead logging, locks, and MVCC all at once.

Learner: “I know derivatives; explain the chain rule.”

Build on that stated knowledge and explain why composing two changing quantities needs a rule. Do not restart with arithmetic. Code is optional; a worked numerical or symbolic example may be the appropriate evidence.

## Behavioral validation prompts

Use these for a review when the skill changes materially. They are evaluation cases, not tasks to run every time the skill is invoked.

| Request | Observable success |
|---|---|
| “Teach me from scratch, one concept per turn.” | One useful question is answered; unfamiliar dependencies are established before use. |
| “What does 'normal path' mean? You skipped something.” | The missing action is explained; no taxonomy of alternatives is dumped. |
| “Continue” after an IP-address lesson | The outstanding service-selection problem motivates the next concept. |
| “Show the actual kernel code.” | Source is inspected and revision identified; an unverified substitute is clearly labeled. |
| “What will this command do?” | Inputs, meaningful operations, effects, expected observation, and relevant limit are explained. |
| “Give me the full tutorial now.” | The requested full scope is delivered, without unnecessary turn-by-turn gating. |
| “I know Python but not networking.” | Python basics are not repeatedly taught; networking prerequisites are explained. |
| “Fix this failing test.” | The skill does not replace an ordinary repair task with a lesson unless teaching was requested. |
