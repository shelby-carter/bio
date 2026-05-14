I'm the author of **[Lixpi](https://github.com/Lixpi/lixpi)** an AI-powered graphic editor for image and video generation. It's not a traditional editor like Photoshop or Premiere. it looks more like an AI concept board where an artist runs their entire creative workflow on an infinite canvas. Technically, it's a visual, node-based workflow engine for AI image and video pipelines, where the spatial arrangement of nodes *is* the workflow.

A few things make it unusual.

The node-based canvas lets you lay out an entire generation pipeline as a topology. Images, documents, and AI chat threads are nodes, directional edges between them define what feeds into what. Rearranging the canvas rearranges the workflow.

The second piece is **feature extraction**. A "feature" is any reusable abstraction pulled out of one or more reference inputs - a texture, a drawing style, a stroke pattern, a lighting setup, a time period, a genre, or something more abstract like mood or atmosphere. Once extracted, you reference features in plain language inside any prompt, and you can mix and match them freely. Each feature is stored as a small set of graphic artifacts (the minimal reusable building blocks) together with a written skill that tells the model what's encoded in those samples and how to apply them. Stacking and chaining features is what gives you character consistent generation across many scenes, the hard problem that text prompts alone cannot solve.

When you trigger image or video generation, it isn't a one-shot call. The prompt first runs through an enhancement stage where a strong reasoning model expands your input into a detailed brief, and that brief is what the media model actually receives.

---

I presented an early prototype at the **AI Tinkerers Toronto** science fair in April 2026, hosted by **Shopify**.

There's also a release announcement on **YouTube**: [https://www.youtube.com/watch?v=Eee2Ku-Tl_8](https://www.youtube.com/watch?v=Eee2Ku-Tl_8) but it's already quite outdated. The product has moved a long way since then, and the next announcement video is about a month out.

Later this month during Tech Week I'll be showing the project at several events, including **"AI Gatherings"** hosted by **Google for Startups Accelerator**.

Some of the features described above are still in development and currently live only on the `develop` branch or in open pull requests. Reach out if you'd like to see a live demo.

---

**Tech stack**

- **LangGraph** - AI workflow orchestration
- **NATS / NATS JetStream** - messaging backbone for the entire system (end-to-end communication and object storage)
- **PIXI.js, @xyflow/system, D3, Svelte** - infinite canvas UI
- **ProseMirror, CodeMirror** - rich-text editors for AI chat and prompt input
- **DynamoDB** - persistence
- **Pulumi, AWS** - cloud deployment (largely cloud-agnostic today; the plan is to go fully cloud-agnostic by swapping DynamoDB for Cassandra)
- **LLM / media APIs** - OpenAI, Anthropic, Google, Stable Diffusion, Bytedance (Seedance 2)
- **TypeScript** - the main language across the project. The current preview release still includes one Python service; that gets replaced by a TypeScript implementation in the upcoming release.

**Source**
- Repo: [https://github.com/Lixpi/lixpi](https://github.com/Lixpi/lixpi)


---

Another project of mine is **[@lixpi/markdown-stream-parser](https://github.com/Lixpi/markdown-stream-parser)** an **incremental markdown stream parser** a library that parses an LLM response token by token and emits styled segments in real time. It's one of the foundational pieces inside Lixpi (it drives the live-styled chat output), but it lives as a standalone open-source package and stays render-agnostic, it emits parsed segments with their styles, and the consumer decides how to draw them.

The current release uses a custom state machine with regex pattern matching. In the next version, my friend and business partner and I are replacing that with **Tree-sitter**, which handles incremental parsing and malformed input gracefully, exactly what you want for the "probabilistic markdown" LLMs produce.

- Repo: [https://github.com/Lixpi/markdown-stream-parser](https://github.com/Lixpi/markdown-stream-parser)
- Tree-sitter migration discussion: [https://github.com/Lixpi/markdown-stream-parser/pull/10](https://github.com/Lixpi/markdown-stream-parser/pull/10)
