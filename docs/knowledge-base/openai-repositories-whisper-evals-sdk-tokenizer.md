# OpenAI repositories — extracted knowledge

Source repositories:
- openai/whisper
- openai/evals
- openai/openai-python
- openai/tiktoken
- openai/openai-node

## 1. Whisper

Whisper is a general-purpose speech recognition model trained on diverse audio. It supports multilingual speech recognition, speech translation, language identification, and voice activity detection. Its architecture is a Transformer sequence-to-sequence model where the multitask objectives are represented as token sequences with special task/control tokens.

### Operational model
- Audio is processed through a sliding 30-second window during `transcribe()`.
- Lower-level APIs expose audio loading, padding/trimming, log-Mel spectrogram creation, language detection, and decoding.
- CLI supports transcription and language selection.
- Multilingual models can translate non-English speech to English.
- The `turbo` model is optimized for fast transcription but is not trained for translation; for translation use multilingual `tiny`, `base`, `small`, `medium`, or `large` models.

### Model trade-offs from the source README
| Model | Params | Approx VRAM | Relative speed vs large |
|---|---:|---:|---:|
| tiny | 39M | ~1GB | ~10x |
| base | 74M | ~1GB | ~7x |
| small | 244M | ~2GB | ~4x |
| medium | 769M | ~5GB | ~2x |
| large | 1550M | ~10GB | 1x |
| turbo | 809M | ~6GB | ~8x |

English-only `.en` models tend to perform better for English, especially tiny/base. Performance varies by language and should be assessed with WER/CER; translation quality can be evaluated with BLEU.

Dependencies include PyTorch, `tiktoken`, and the `ffmpeg` command-line tool. A Rust toolchain may be needed where a prebuilt `tiktoken` wheel is unavailable.

## 2. OpenAI Evals

Evals is a framework for evaluating LLMs and LLM-based systems. Core concepts:
- An eval consists of a dataset plus an eval class/template.
- Prefer reusable existing templates when possible.
- Dataset samples are JSONL objects; all templates expect an `input` field.
- Basic `Match`, `Includes`, and `FuzzyMatch` evals also use an `ideal` reference.
- Model-graded evals are configured with evaluation prompts/YAML and can avoid custom evaluation code.
- Eval names follow `<eval_name>.<split>.<version>`; bump the version when the eval changes so results remain reproducible/comparable.
- Evaluation quality criteria: thematic consistency, challenge, clear directional signal, high-quality references/rubrics, careful prompt/template selection, and spot checking.
- Useful targets include safety, over-refusal, steerability, hallucination, reasoning, and real-world product use cases.

### Typical workflow
1. Build/normalize a JSONL dataset.
2. Register the eval and its metrics/template.
3. Run with the CLI/model or completion function.
4. Iterate until results are trustworthy.
5. For model-graded evals, add a meta-eval with human-provided choice labels to validate the grader itself.

The repository also supports private/internal eval data and an existing registry. Costs of API-based evaluations must be considered.

## 3. OpenAI Python SDK

The Python SDK is the generated, typed client for the OpenAI REST API. Source README states Python 3.10+ and synchronous/asynchronous clients based on HTTPX2.

### Core API patterns
- `OpenAI()` for synchronous use.
- `AsyncOpenAI()` for asynchronous use.
- Responses API is the primary model interface in the current SDK.
- Chat Completions remains supported.
- `response.output_text` is the convenient text surface.
- Image inputs can be provided by URL or base64 data URL through Responses API.
- SSE streaming is supported with `stream=True`.

### Authentication
Prefer environment-managed credentials rather than hard-coding secrets. The SDK also documents workload identity with short-lived credentials for Kubernetes, Azure managed identity, GCP, custom subject-token providers, and X.509 workload identity. X.509 is tied to configured mTLS transport and does not cover Realtime/WebSockets in the documented Python integration.

### Realtime
The SDK exposes a WebSocket-based Realtime API for low-latency multimodal interactions, including text/audio I/O and function calling. Client and server events form the protocol. Important operational rule: Realtime API errors arrive as `error` events while the connection remains open; applications must explicitly handle them.

### Types and pagination
- Nested request parameters use `TypedDict`.
- Responses use Pydantic models.
- Models offer JSON/dict serialization helpers.
- List endpoints provide automatic pagination iterators, plus explicit page navigation helpers.

## 4. tiktoken

`tiktoken` is OpenAI's fast BPE tokenizer.

### Core properties
- Reversible/lossless tokenization.
- Works on arbitrary text.
- Compresses input into fewer tokens than raw bytes.
- BPE exposes reusable common subwords, improving statistical generalization.
- Model-specific encodings can be obtained through `encoding_for_model()`; generic encodings via `get_encoding()`.

### Engineering implications
- Tokenization should be treated as a first-class context/cost constraint in agent systems.
- Token counts matter for context budgeting, prompt design, caching, evaluation cost, and long-running agent reliability.
- `tiktoken` is optimized for throughput and the source reports 3–6x speed over a comparable open-source tokenizer in its benchmark.
- Custom encodings can be instantiated directly with `Encoding` or registered through the `tiktoken_ext` namespace plugin mechanism.

## 5. OpenAI Node/TypeScript SDK

The Node SDK is a generated TypeScript/JavaScript client for the REST API. It is designed around the Responses API while retaining Chat Completions support.

### Core patterns
- `npm install openai`.
- `new OpenAI({ apiKey: process.env.OPENAI_API_KEY })`.
- Responses API with `instructions`, `input`, and `response.output_text`.
- Vision through `input_image` plus text content.
- SSE streaming via async iteration.
- File uploads accept web `File`, `fetch` `Response`, `fs.ReadStream`, or `toFile`/`toStreamingFile` helpers.

### Conversation state
When manually replaying Responses state, preserve the full ordered set of replayable output items. Filtering only to messages can omit required reasoning/tool-call items. `toResponseInputItems()` normalizes replayable items; `previous_response_id` is the simpler continuation mechanism.

### Authentication
Node SDK documents workload identity for Kubernetes, Azure, GCP, custom JWT providers, and X.509 client certificates. X.509 support uses certificate-backed credentials and controlled mTLS transport.

### Realtime
Node exposes the WebSocket Realtime API for low-latency multimodal interactions and function calling.

### Webhooks
Webhook verification is explicitly encouraged. Verify the raw request body before trusting or parsing the event; `client.webhooks.unwrap()` verifies and parses, while `verifySignature()` verifies only. Do not parse the body before signature verification.

### Errors, retries, timeouts
- HTTP/API failures map to typed subclasses such as authentication, permission, not found, conflict, rate-limit, server, and connection errors.
- SDK retries certain transient failures by default, including connection errors, 408, 409, 429, and 5xx.
- Request timeout defaults to a long window and is configurable globally or per request.
- Responses expose `_request_id`; this is useful for debugging and support correlation.

### Pagination and provider support
- Async iteration can walk paginated list endpoints.
- Single-page controls are also available.
- The SDK has documented integrations for Azure OpenAI and Amazon Bedrock through provider-specific configuration.

## Cross-repository engineering lessons

1. **Audio is a subsystem, not merely an input format.** Whisper shows that speech recognition, translation, language detection, and VAD can share a multitask model, while Agents/Realtime layers provide the realtime orchestration surface.
2. **Evaluation must be part of the agent lifecycle.** Evals establishes datasets, reusable templates, reproducibility, model-graded evaluation, and meta-evaluation; the Cookbook adds trace → feedback → eval → harness iteration.
3. **Typed SDK boundaries reduce integration errors.** Both Python and Node clients are generated from OpenAPI and expose typed request/response surfaces.
4. **Continuation must preserve semantic state, not just chat messages.** Responses output can contain reasoning/tool items that are necessary for correct replay.
5. **Security belongs around credentials and side effects.** Prefer environment/workload identity, verify webhooks before trust, correlate requests with IDs, and keep sensitive data out of logs.
6. **Resilience needs explicit retry policy.** SDK-level retries are useful for transient failures but must respect replay safety for stateful or side-effecting operations.
7. **Tokenization is an infrastructure concern.** Token budgets affect context trimming, model cost, latency, caching, eval budgets, and memory strategies.
8. **Streaming and realtime require event-oriented error handling.** Applications should model streams as stateful event flows, not simple request/response calls.
9. **Prefer generated/official clients and stable abstractions.** They reduce drift between application code and API schemas and make versioned behavior explicit.
10. **Use the smallest abstraction that fits.** Direct SDK calls work for simple model interaction; Agents SDK adds the run loop/orchestration; sandbox/realtime/evals layers should be introduced where their specific execution or quality needs justify them.
