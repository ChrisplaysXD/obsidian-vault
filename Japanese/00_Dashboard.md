---
cssclasses:
  - cards
banner: "https://images.unsplash.com/photo-1493976040374-85c8e12f0c0e?q=80&w=1200&auto=format&fit=crop"
---

<img src="https://images.unsplash.com/photo-1493976040374-85c8e12f0c0e?q=80&w=1200&auto=format&fit=crop" class="notion-cover" alt="Japanese Garden Banner" />

# 🎌 Japanese Learning Space

> [!NAV] Navigation
> [[Home|🏠 Central Knowledge Base]] ⸱ [[Japanese Language MOC|🗺️ Japanese Language MOC]]

> [!TIP] The Moe Way Focus & Ratio Rule
> **Target Ratio**: 70% Listening / Immersion ⸱ 30% Grammar & Reading  
> **Daily Micro-Goal**: 10 new Anki cards (Kaishi 1.5k), keep Renshuu streak alive, 15m audio shadowing.

---

## ⚡ Quick Launchers & Resources
| Ecosystem | Launch Links | Notes |
|---|---|---|
| **Daily Habit Tools** | [Renshuu](https://www.renshuu.org) ⸱ [AnkiWeb](https://ankiweb.net) | Grammar progression & core vocab SRS |
| **Lookup & Dictionaries** | [Jisho.org](https://jisho.org) ⸱ [Yomitan Guide](https://learnjapanese.moe/yomichan/) | Instant popup lookups & 1T card mining |
| **Audio Immersion** | [Nihongo con Teppei](https://nihongoconteppei.com) ⸱ [Comprehensible JP](https://cijapanese.com) | Level 1 & 2 listening with solo shadowing |
| **Grammar References** | [Cure Dolly Transcripts](https://kellenok.github.io/cure-script/) ⸱ [Tae Kim Guide](https://guidetojapanese.org/learn/) | Structural models and particle nuance |

---

## 🗺️ Roadmap & Curricula Quick Access
- 📝 [[Kana_Mastery|Hiragana & Katakana Checklist]]
- 🔄 [[TMW_Beginner_Loop|The Moe Way Study Loop & Milestones]]
- 🎯 [[JLPT_N5_Roadmap|JLPT N5 Core Grammar & Vocab Checklist]]
- 🚆 [[Travel_Phrases_Index|Survival Japanese for Travel & Daily Life]]

---

## 📊 Recent Study & Immersion Logs (Last 7 Days)
```dataview
TABLE 
    active_immersion_min AS "Active (min)", 
    passive_immersion_min AS "Passive (min)", 
    shadowed_duration_min AS "Shadowing (min)", 
    renshuu_completed AS "Renshuu?", 
    anki_reviews_done AS "Anki?"
FROM "Japanese/05_Journal/Daily"
WHERE type = "daily_log"
SORT date DESC
LIMIT 7
```

---

## 🎧 Recent Audio Immersion & Shadowing Sessions
```dataview
TABLE 
    source_type AS "Source", 
    duration_min AS "Duration (min)", 
    listening_level AS "Listening Level", 
    shadowed AS "Shadowed?"
FROM "Japanese/01_Immersion/Active_Logs"
WHERE type = "immersion_log"
SORT file.mtime DESC
LIMIT 5
```

---

## ⛏️ 1T Mined Vocabulary & Kaishi Stash
```dataview
TABLE 
    reading AS "Reading", 
    meaning AS "Meaning", 
    jlpt AS "JLPT", 
    anki_synced AS "In Anki?", 
    status AS "Status"
FROM "Japanese/02_Vocabulary"
WHERE type = "vocabulary"
SORT file.mtime DESC
LIMIT 10
```

---

## 📖 Active Grammar Points & Particle Nuances
```dataview
TABLE 
    meaning AS "Meaning", 
    formation AS "Formation", 
    pitfall_warning AS "Pitfall Alert"
FROM "Japanese/03_Grammar"
WHERE type = "grammar" AND status = "active"
SORT file.name ASC
```

---

## 📌 Sticky Notes & Rapid Captures
- [ ] Configure Anki Kaishi 1.5k: max reviews to 9999, new cards to 10/day.
- [ ] Install Yomitan on Chrome/Brave/Firefox with JMdict & Kanjidic.
- [ ] Finish shadowing Teppei Beginner Ep 1 to 5.
