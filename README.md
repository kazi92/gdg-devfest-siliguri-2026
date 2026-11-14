# Building Leonida for Real 🏙️
### The intelligence layer that makes industries aware — on Google Cloud

**GDG DevFest Siliguri · 14 November 2026 · Kazi Haque**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kazi92/gdg-devfest-siliguri-2026/blob/main/notebooks/mini_leonida.ipynb)

In GTA VI, the city of Leonida feels alive because everything in it is aware of everything else. A crash causes a jam, police respond, pedestrians scatter.
Real buildings, campuses and industrial parks collect plenty of data, but their systems rarely talk to each other.
This repo has everything from the session so you can build your own **mini-Leonida** with free tools.

---

## 🚀 Start here

| I want to… | Go to |
|---|---|
| Run the hands-on notebook (Colab, free) | [`notebooks/mini_leonida.ipynb`](notebooks/mini_leonida.ipynb) or the **Open in Colab** badge above |
| Try the live-demo prompt in Google AI Studio | [`prompts/demo_prompt.md`](prompts/demo_prompt.md) |
| Use the data in my own project | [`data/`](data/) |

You need a free Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey). No key? The notebook still runs with a sample answer.

---

## 🧠 The idea in one picture

A living world needs three layers:

| Mission | Layer | Question it answers | Google building blocks |
|---|---|---|---|
| 1 | **The map** | What exists, and what state is it in? | Edge gateway → Pub/Sub → BigQuery · Maps Platform Weather & Routes APIs |
| 2 | **Relationships** | Who affects whom? | [Digital Buildings Ontology](https://google.github.io/digitalbuildings/) · Spanner Graph · BigQuery Graph |
| 3 | **Awareness** | Why did it happen, and what should we do? | Gemini · RAG over SOPs · [ADK](https://google.github.io/adk-docs/) agents on Gemini Enterprise Agent Platform · Gemma on-prem · Gemini Live API |

**Data flow:** sensors and building systems → edge gateway → Pub/Sub → BigQuery (history) + Spanner Graph (relationships) + Weather API (outside world) → Gemini agent (+ SOPs via RAG) → a human approves → the action flows back to the site.

---

## 🏫 The scenario: one event day on a campus

At 10:40 the condenser pump on chiller **CH-2** starts losing flow. Chilled water warms from 7 °C to 12 °C. The **Main Hall**, with 600 people inside, climbs past 29 °C, and at the end everyone heads for **Gate 1** at once.

Every dashboard still says **RUNNING**. The cause and the symptom live in different systems, so only something that understands the relationships can connect them.

---

## ⭐ The wanted-level ladder: how much should the AI decide?

| Level | Mode | The AI… |
|---|---|---|
| ★ | Observe | flags drift |
| ★★ | Recommend | suggests; a human decides |
| ★★★ | Act on approval | acts after a human taps yes |
| ★★★★ | Act and report | acts, then explains |
| ★★★★★ | Autonomous | no human in the loop |

Most buildings should live at **★★ to ★★★**. Fire, life safety and crowd control never climb higher. Decide the star level for each decision **before** you build the agent, and enforce it in code, not in the prompt. The notebook shows how.

---

## 🎮 Weekend build: your own mini-Leonida

1. **Simulate:** a chiller, an air handler and one room in Colab, with one slow drift you hide on purpose.
2. **Relate:** describe how they connect, with the Digital Buildings Ontology or a small JSON graph.
3. **Reason:** ask Gemini in AI Studio, “Why is this room getting hot?”
4. **Go offline:** run the same prompt on Gemma on your laptop. That's your first air-gapped AI.

**Stretch goal:** wrap it in an ADK agent that opens a mock maintenance ticket, and decide its star level first.

Side quests are at the end of the notebook. Share what you build with **#DevFestSiliguri**!

---

## 📁 What's in this repo

```
notebooks/mini_leonida.ipynb   Hands-on notebook: map → graph → Gemini agent → guardrail
prompts/demo_prompt.md         The exact prompt and data from the live demo (paste into AI Studio)
data/campus_telemetry.csv      Synthetic telemetry: chiller, air handler, hall, people, weather
data/campus_graph.json         Who-affects-whom graph (nodes + FEEDS / SERVES / OCCUPIES / EXITS_VIA edges)
data/sop_fm_04.json            The facility rules the agent must respect
data/weather_forecast.json     A forecast shaped like the Maps Platform Weather API
```

All data is synthetic and made for learning.

---

## 📚 Resources

- [Google AI Studio](https://aistudio.google.com/): get an API key and try prompts
- [Gemini API docs](https://ai.google.dev/gemini-api/docs)
- [Gemma open models](https://ai.google.dev/gemma)
- [Agent Development Kit (ADK)](https://google.github.io/adk-docs/)
- [Digital Buildings Ontology (Google, open source)](https://google.github.io/digitalbuildings/)
- [Spanner Graph](https://cloud.google.com/spanner/docs/graph/overview)
- [Google Maps Platform Weather API](https://developers.google.com/maps/documentation/weather/overview)
- [BigQuery](https://cloud.google.com/bigquery) and [Pub/Sub](https://cloud.google.com/pubsub)

---

## 👋 Connect

**Kazi Haque**: Founder, Kernopy · GDG Mentor
[LinkedIn](https://www.linkedin.com/in/haquekazi/) · [kazihaque.dev](https://kazihaque.dev)

If you could make one thing on your campus aware, what would it be? Build it, and tell me about it.

*Licensed under MIT. Use it, remix it, run it at your own GDG.*
