# Kader Mula (@mulak1)

**Full-Stack Software Engineer, Systems Contributor & Design Systems Architect**  
San Francisco Bay Area, CA · San Francisco State University · [mulak1@gmail.com](mailto:mulak1@gmail.com) · [exactbaseline.com](https://exactbaseline.com)

I build concurrent backend systems, developer tools, vector SVG/print design systems, and technical documentation in Scala (ZIO), Go, TypeScript, Python, and React. Across open-source contributions and client work, I focus on surgical, well-tested pull requests with clear root-cause analysis, binary compatibility verification, and zero unrelated diff noise.

## Core Stack & Capabilities

* **Languages & Runtimes:** Scala (2.12 / 2.13 / 3.3, ZIO, ZStream, ZIO HTTP, ZIO Schema), Go, TypeScript / JavaScript (Node.js, Bun), Python, SQL, HTML/CSS, SVG
* **Concurrency & Distributed Systems:** Lock-free data structures (`AtomicReferenceArray`, `ReferenceQueue`), Project Loom virtual-thread safety, backpressured streaming pipelines, HTTP/RPC middleware, LLM gateway billing & security controls
* **Frontend, Vector & Print Design Systems:** React, Next.js, Tailwind CSS, Vector SVG/Canvas Rendering, Print & Packaging Dielines (`300 DPI` CMYK, 100% K barcode ink traps, multi-ratio social carousels)
* **Testing & Verification:** ZIO Test, JMH Benchmarks, MiMa Binary Compatibility, Go Test (`httptest`), Vitest, Playwright, Pytest, Property-Based Testing, GitHub Actions CI

## Selected Open-Source Contributions & Systems Engineering

<table>
  <thead>
    <tr>
      <th align="left">Repository &amp; Pull Request</th>
      <th align="left">Stack</th>
      <th align="left">Architectural Scope &amp; Root-Cause Fix</th>
      <th align="left">Verification &amp; CI Proof</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://github.com/zio/zio/pull/11418"><strong><code>zio/zio#11418</code></strong></a></td>
      <td>Scala 2.12 / 2.13 / 3.3</td>
      <td><strong>Loom-Friendly Lock-Free <code>FiberSet</code> (<code>#8861</code>):</strong> Replaced <code>Collections.synchronizedSet(WeakHashMap)</code> in <code>FiberRuntime._children</code> with a lock-free <code>AtomicReferenceArray</code> strong-reference nursery + <code>ReferenceQueue</code> weak set to prevent virtual-thread pinning.</td>
      <td><code>FiberSetSpec</code> + <code>FiberSetBenchmark</code> (JMH), CLA signed</td>
    </tr>
    <tr>
      <td><a href="https://github.com/zio/zio/pull/11417"><strong><code>zio/zio#11417</code></strong></a></td>
      <td>Scala 2.12 / 2.13 / 3.3</td>
      <td><strong>Unbounded <code>ZStream#mapZIOPar</code> Parallelism (<code>#9339</code>):</strong> Decoupled worker fiber concurrency (<code>n</code>) from output queue capacity (<code>bufferSize</code>) in <code>ZChannel.mergeAllWith</code> by bounding <code>permits: Semaphore</code> to <code>n</code> while preserving downstream backpressure via <code>queue.offer</code>.</td>
      <td><code>16/16</code> JVM (17/21/25), Scala.js &amp; Scala Native CI checks passing</td>
    </tr>
    <tr>
      <td><a href="https://github.com/zio/zio/pull/11419"><strong><code>zio/zio#11419</code></strong></a></td>
      <td>Scala 2.12 / 2.13 / 3.3</td>
      <td><strong>Cooperative Yielding in <code>ZStream.groupedWithin</code> (<code>#8686</code>):</strong> Fixed timer-fiber starvation on infinite streams emitting empty chunks (<code>in.isEmpty</code>) by yielding via <code>ZIO.yieldNow</code> in <code>handoffProducer</code> before recursing.</td>
      <td><code>ZStreamSpec</code> regression suite, <code>lint</code> + <code>2.12/2.13/3.3/JS/Native</code> passing</td>
    </tr>
    <tr>
      <td><a href="https://github.com/zio/zio-http/pull/4389"><strong><code>zio/zio-http#4389</code></strong></a></td>
      <td>Scala 2.12 / 2.13 / 3.3</td>
      <td><strong><code>HandlerAspect</code> + Path Parameter Composition (<code>#3141</code>):</strong> Widened <code>Handler.IsRequest</code> implicit evidence from <code>In &lt;:&lt; Request</code> to <code>Request &lt;:&lt; In</code> via <code>contramap[(Path, Request)](_._2)</code> so <code>RoutePattern</code> tuple extractors compose with <code>Middleware</code> without <code>ClassCastException</code>.</td>
      <td><code>9/9</code> Build &amp; Test matrix jobs + <code>MiMa Check</code> + <code>fmtCheck</code> + <code>mdoc</code> passing</td>
    </tr>
    <tr>
      <td><a href="https://github.com/zio/zio-schema/pull/1255"><strong><code>zio/zio-schema#1255</code></strong></a></td>
      <td>Scala 2.12 / 2.13 / 3.3</td>
      <td><strong>Strict Top-Level JSON Trailing-Token Rejection (<code>#712</code>):</strong> Enforced end-of-input whitespace consumption in <code>JsonCodec.JsonDecoder.decode</code> so malformed trailing characters (<code>{"a":1}extra</code>) fail deterministically while streaming <code>JsonSplitter</code> remains intact.</td>
      <td><code>28/28</code> GitHub Actions checks passing (<code>MiMa</code>, <code>Lint</code>, <code>18</code> JVM/JS/Native jobs)</td>
    </tr>
    <tr>
      <td><a href="https://github.com/hanzoai/ai/pull/154"><strong><code>hanzoai/ai#154</code></strong></a></td>
      <td>Go (<code>package controllers</code>)</td>
      <td><strong>LLM Gateway Billing &amp; Token Accuracy QA (<code>#136</code>):</strong> End-to-end verification of <code>Get ModelPrice</code> (<code>k=1,000</code> vs <code>m=1,000,000</code> divisor math), SSE streaming usage accumulation, and <code>relayWorld</code> zero-charge (<code>0.000000 USD</code>) invariant on upstream <code>500</code>/<code>429</code> errors.</td>
      <td><code>controllers/billing_token_accuracy_qa_test.go</code> (<code>3/3</code> suites passing, CI green)</td>
    </tr>
    <tr>
      <td><a href="https://github.com/hanzoai/ai/pull/155"><strong><code>hanzoai/ai#155</code></strong></a></td>
      <td>Go (<code>package controllers</code>)</td>
      <td><strong>Multimodal Security &amp; Authz Gate QA (<code>#135</code>):</strong> Verified <code>messagesToOpenAI</code> system-prompt hierarchy under SVG/XSS/EXIF/path-traversal payloads, <code>fits</code>/<code>MaxTranscribeUpload</code> audio limits, and ZAP <code>securityGroupMethods</code> authz gates.</td>
      <td><code>controllers/multimodal_security_qa_test.go</code> (<code>3/3</code> suites passing, CI green)</td>
    </tr>
    <tr>
      <td><a href="https://github.com/TheSolaAI/sola-application/pull/511"><strong><code>TheSolaAI/sola-application#511</code></strong></a></td>
      <td>TypeScript / React</td>
      <td><strong>Handsfree Solana Actions / Blinks Execution (<code>#157</code>):</strong> Added <code>executeActionBlink</code> tool to the <code>aikit</code> voice agent toolset (<code>GET</code> Action metadata, <code>POST</code> user pubkey, sign &amp; broadcast base64 VersionedTransaction) + <code>BlinkExecutionMessageItem</code> UI card.</td>
      <td><code>7/7</code> unit tests passing (<code>tests/blinks.test.cjs</code>), <code>Sourcery review</code> passing</td>
    </tr>
  </tbody>
</table>

## Flagship Projects & Open-Source Repositories

### 1. [ExactBaseline Decision Calculators](https://exactbaseline.com)
Deterministic financial and operational planning calculators with zero-auth JSON-RPC 2.0 Model Context Protocol (MCP) endpoints:
* **[RateRecast (Mortgage Recast vs. Reinvest)](https://exactbaseline.com/calculator/mortgage_recast):** Fannie Mae F-1-05 lump-sum amortization simulator and after-tax treasury comparison.
* **[BarStock (Event Beverage Estimator)](https://exactbaseline.com/calculator/bar_stock):** Liquor, wine, and beer estimator across 950+ event configurations.
* **[CarFloor (Used Vehicle Out-The-Door Cost)](https://exactbaseline.com/calculator/auto_depreciate):** Wholesale depreciation curves, dealer holdbacks, and state DMV doc-fee caps.
* **[PaceForge (Marathon Negative-Split Planner)](https://exactbaseline.com/calculator/pace_forge):** Jack Daniels VDOT pacing and split-clock schedules.

### 2. [PulseForge AI: Developer Infrastructure Benchmarks](https://exactbaseline.com/leaderboard)
Empirical latency, throughput, and cost benchmarks across open-source developer tools and AI infrastructure:
* **[Benchmark Categories](https://exactbaseline.com/benchmarks):** [AI Coding Agents](https://exactbaseline.com/benchmarks/ai-coding-agents) · [Vector Databases](https://exactbaseline.com/benchmarks/vector-databases) · [LLM Inference Engines](https://exactbaseline.com/benchmarks/llm-inference-engines) · [Open-Source S3 Storage](https://exactbaseline.com/benchmarks/open-source-s3-object-storage-data-lake-minio-seaweedfs) · [Infrastructure as Code](https://exactbaseline.com/benchmarks/open-source-infrastructure-as-code-iac-terraform-alternatives) · [Container Registries](https://exactbaseline.com/benchmarks/open-source-container-registries-artifact-repositories)
* **[Token FinOps Calculator](https://exactbaseline.com/token-calculator):** Seat-license vs. direct API token break-even modeling for engineering teams.

### 3. [Open-Source MCP Servers & Datasets](https://github.com/mulak1?tab=repositories)
* **[Awesome Developer Benchmarks](https://github.com/mulak1/awesome-developer-benchmarks):** Reproducible latency distributions and benchmark harnesses across 97 software infrastructure categories (MIT License).
* **[Open CIELAB Cosmetics Dataset](https://github.com/mulak1/open-cielab-cosmetics-dataset):** CIE L\*a\*b\* (D65) spectrophotometric cosmetics dataset (121 shades, CIEDE2000 dupe matrices, and 12-Season Color Analysis palettes).
* **[ClauseGuard MCP](https://github.com/mulak1/clauseguard-mcp) · [BillTally MCP](https://github.com/mulak1/billtally-mcp) · [DeckForge MCP](https://github.com/mulak1/deckforge-mcp):** Remote Model Context Protocol (MCP) connectors for contract redlining, invoice verification, and executive slide deck generation.
