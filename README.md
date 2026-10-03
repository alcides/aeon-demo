# Aeon in your browser

Aeon is a small programming language with refinement types, SMT-backed
verification, and program synthesis. This repository is a ready-to-run demo:
open it in a browser-based development environment, edit an `.ae` file, and
run it in the terminal.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/alcides/aeon-demo)
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/alcides/aeon-demo)

Both options start VS Code in the browser with the Aeon language extension,
Python, Z3, and the `aeon` command pre-installed. No local setup is required.

## Try it

1. Open this repository in Codespaces or Gitpod using one of the buttons above.
2. Open [`hello.ae`](hello.ae).
3. Run the file in the integrated terminal:

   ```bash
   aeon hello.ae
   ```

   It should print `4`.

4. Change `a + 1` to `a - 1` and run it again. Aeon rejects the program because
   its refinement type promises a result greater than the input.

The quickest next examples are in [`examples/llm_talk`](examples/llm_talk):

| Example | Demonstrates |
| --- | --- |
| `1_types_are_not_enough.ae` | Why ordinary types do not prevent every bug |
| `2_refinements.ae` | Refinement types and compile-time guarantees |
| `3_uninterpreted.ae` | Talking about opaque/native values |
| `7_synthesis.ae` | Filling a `?hole` with synthesis |
| `8_llm_plus_refinements.ae` | Using an LLM behind a refinement contract |

Run one with:

```bash
aeon examples/llm_talk/2_refinements.ae
```

For the deterministic synthesis example:

```bash
aeon -s synquid examples/llm_talk/7_synthesis.ae
```

The LLM example requires a local Ollama installation and model, so it is
included as an optional advanced example rather than part of the startup path.

## Local development

With Python 3.11+ and [uv](https://docs.astral.sh/uv/) installed:

```bash
uv venv
uv pip install aeonlang
uv run aeon hello.ae
```

The browser environments use the same installation flow through their
container definitions in [`.devcontainer`](.devcontainer) and [`.docker`](.docker).

## What this demo is for

This is intentionally a small teaching workspace, not a copy of Aeon's full
source tree. It gives newcomers a working editor and a handful of examples
that show the progression from ordinary types, to refinements, to verification
and synthesis. See the [Aeon repository](https://github.com/alcides/aeon) for
the compiler, full standard library, and complete documentation.
