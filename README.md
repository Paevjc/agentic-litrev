I want to conduct a short literature review on Agentic AI and its workflows. I will be having a hybrid of artisanal / ai-assistance coding. Some goals I have in mind are:
- Memory types and systems (Working, Episodic, Semantic, Procedural)
- API tool calling (simple use-case: Singapore current status on weather/temp/psi)
- Google ADK
- Some multi-agent orchestration (?)

README is not conclusive and definitely not presentable... Will fix after literature review conclude.

qns ─► answer(qns)
        │
        ├─ 1. resolve_place(qns)        "Where do you mean?"         2 LLM + 1 API call
        │     ├─ 1a extractor   [LLM]   qns       → "Tampines"
        │     ├─ 1b geocode     [API]   "Tampines" → 5 candidates
        │     ├─ 1c picker      [LLM]   candidates → "0"
        │     └─ 1d guardrail   [code]  "0" → p (+ nearest_region → "east")
        │
        ├─ 2. verify_place(qns, p)      "Did we get it right?"       1 LLM call
        │     └─ YES → continue  |  NO → return "I'm not sure..." ■
        │
        ├─ 3. gather(p)                 "What's it like there?"      4 API calls, no LLM
        │     └─ fetches + bands + recommend() → facts
        │
        └─ 4. write_checked_report(facts) "Tell the user"            1+ LLM calls
              └─ loop: write_report [LLM] → check_report [code] → pass / retry / raise