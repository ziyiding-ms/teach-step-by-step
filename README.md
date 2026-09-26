# Teach Step by Step · 不跳步教学

An Agent Skill for explanations that introduce **why a concept is needed before what it is**, build on the learner's actual knowledge, and connect small examples to observable results.

让每一个新概念都有来由：先说明当前遇到的问题，再介绍解决它的机制；例子和代码要解释输入、动作、结果与适用范围。“继续”接着上次尚未解决的问题讲，不重启课程、不突然堆术语。

## What it changes

- **Problem before terminology:** expose the missing capability or ambiguity before naming a mechanism.
- **No hidden prerequisites:** explain the concrete action before labels such as “ordinary copy send path.”
- **Pacing that follows the request:** one main question per turn for interactive lessons; a complete ordered explanation when the learner asks for it.
- **Code that teaches:** say what it will do before presenting it, explain meaningful operations, and interpret the result.
- **Honest evidence:** distinguish expected output, actual observations, simulations, and verified implementation source.
- **Continuity:** remember what has been established, repair missing dependencies, and resume the next question.

This is a general teaching method, not a TCP textbook or a requirement to use code for every subject. It does not force quizzes, add tools, or turn ordinary implementation requests into lessons.

## Use

Explicit prompt:

```text
Use $teach-step-by-step to explain how TCP recovers lost data.
I know Python but not networking. Explain why each concept is needed,
one step at a time, and explain what any code example will do.
```

中文示例：

```text
用 $teach-step-by-step 从我目前的理解开始讲，不要跳步。
先说为什么需要这个概念，再解释它是什么。
给代码前，先说代码会做什么；我说“继续”时再接着讲。
```

For a complete tutorial, request it explicitly; the skill will preserve the causal order without requiring a new turn for every step.

## Install locally

The repository root is the skill folder. For a Codex setup using personal skills under `~/.codex/skills`, and with no existing folder of this name:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ziyiding-ms/teach-step-by-step.git ~/.codex/skills/teach-step-by-step
```

Then use the skill after the host refreshes its available skills; start a new session if the current session retains an older catalog. If your host uses a different skill directory, put the folder there instead. Other Agent Skills-compatible tools can use `SKILL.md` according to their own installation conventions; automatic discovery varies by host.

No API keys, dependencies, executables, or network services are required by the skill itself. Example commands are run only when useful and within the user's authorized scope.

## Files

| File | Purpose |
|---|---|
| [SKILL.md](SKILL.md) | Teaching workflow, continuation rules, and code/source boundaries |
| [references/teaching-examples.md](references/teaching-examples.md) | Before/after patterns and behavioral review cases |
| [agents/openai.yaml](agents/openai.yaml) | Optional Codex interface metadata |

The examples and instructions are original; the repository does not contain copied kernel source or private conversation transcripts. This is an independent community skill, not an official OpenAI or Anthropic product.

## License

[MIT](LICENSE).
