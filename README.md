# word-memory-tool
AFRO Word Memory Tool (Spaced Repetition Spelling Practice)
A purely local, zero-dependency​ English vocabulary web app AFRO. Two learners can each use different wordbanks, with reviews scheduled along the Ebbinghaus forgetting curve, focusing on spelling​ (first letter as hint; tense/ending inferred by the learner). Learner names can be customized in Settings → Learner Name.
The home page shows only a Daily Overview + Start Button for a clean look; detailed practice modes and PRD notes are all in this README.
How to Open
Simply double-click index.html​ to open it in your browser (Chrome / Edge / Safari all work).
No internet connection or installation required.
Feature-to-PRD Mapping
Two Learners + Separate Wordbanks: Switch between Learner 1 / Learner 2 and KET/PET Core / TOEFL Core at the top; progress is tracked independently. Learner 1 uses a yellow theme. Learner names can be changed in Settings → Learner Name.
Not Just Recognition — Spelling Required​ (auto-advances with proficiency):
Chinese meaning displayed above​ to ensure comprehension; English word partially or fully cloze-tested below​ for spelling practice.
Partial cloze: Target word shows the first letter(s) as hints; complete the spelling (tense/ending inferred by learner); the more proficient, the more letters are hidden.
Full cloze: Entire target word hidden; spell the full word from the Chinese meaning.
Words progress from partial cloze → full cloze. After submission: full English word (highlighted) + POS + definition + related word forms​ (verb: past/past participle/present participle/3rd person singular; noun: singular/plural; adjective: comparative/superlative/adverb, etc.), with 🔊 text-to-speech. Auto-pronunciation plays after submission.
Shortcuts: Space = start/next word; Enter = submit (or next word after revealing answer); ⌘/Ctrl + H = hint.
Ebbinghaus Forgetting Curve: Daily new words (default 25, adjustable 20–30) + review words, total default 45 (adjustable 40–50), estimated 20–30 min per session. Correct answers advance to next review interval (1/2/4/7/15/30 days); mistakes return sooner. No repeats within the same day.
Clean, Kid-Friendly Color Scheme: Rounded cards + bright colors; KET uses orange/blue, TOEFL uses purple/green; Learner 1 is fixed to a yellow theme.
Mining Reward System (inspired by "Math with Ore"): Every correct answer "mines" an ore. Rules — correct = mine ⛏️; longer streaks yield rarer ores (3/5/8/12 consecutive correct answers grant Iron/Gold/Redstone/Lapis Lazuli respectively); correct with hint = Stone; correct after retry = Copper; correct without hint on hard words (★★★) = 💎 Diamond; full session perfect = 🟢 Emerald; cumulative 100/300 correct answers = 🟣 Netherite / 🗼 Beacon; 7-day consecutive practice = 🛡️ Totem of Undying. All ores are permanent collectibles, never deducted. Session end triggers confetti + trophy animation​ and displays ores earned; click 🎁 My Warehouse to view the full ore gallery and cumulative counts, also shown on the Stats page.
Mistake Notebook (Wrong-Word Bank): Incorrect words auto-save to the Mistake Notebook (isolated by learner + wordbank). Click Mistake Notebook at the top to view all wrong words, error counts, and timestamps; click Review These Mistakes for targeted practice; a word is auto-removed once answered correctly once. Updates after each daily session.
Portable: Zip the entire folder and send to others; double-click to use. Wordbanks can be swapped anytime.
📚 KET/PET Wordbank Source: data/ket.js merges the Cambridge KET for Schools Official Wordlist​ and B1 Preliminary (PET) Official Wordlist​ (two PDFs), deduplicated to ~3,100 words. Chinese definitions from ECDICT + manual supplementation. To use your own, see How to Replace Wordbank below.
🗂️ TOEFL Wordbank Source: data/toefl.js is a merged, deduplicated TOEFL high-frequency wordlist (~6,679 words including phrases)​ from Wu Laoshi 1500 / PrepScholar / TOEFL Complete Wordlist. This list contains only English + Chinese definition with no example sentences, so TOEFL practice uses Chinese meaning + standalone cloze word mode (no sentence embedding).
🔊 About Text-to-Speech: Pronunciation uses the browser's built-in speech synthesis (offline, no internet needed). Voice quality depends on English voices installed on your system: macOS includes natural voices like Samantha; on Windows, install and select "Microsoft Aria / David" in Settings → Time & Language → Speech for better results. If unsupported, a prompt will appear.
How to Replace Wordbank
Two methods, choose one:
Method A: In-Page Upload (local only, most convenient)
Go to Wordbank page → click upload → supports .txt / .csv / .json / .js​ formats.
Text format (one per line, comma or tab separated):
apple,苹果
apple,苹果,I eat an apple every day.
JSON format:
[{"en":"apple","zh":"苹果","sentence":"I eat an apple every day."}]
.js format (both recognized):
This tool's format: window.WORDBANKS.toefl = { words:[{en:"apple", zh:"苹果", pos:"n.", sentence:"..."}] }
Third-party format (auto-converts to en/zh, attempts POS inference from definition): const TOEFL_WORDS = [{word:"abandon", meaning:"vt. abandon; give up"}]
Upload only overrides the default wordbank for the current Learner + Wordbank combination; click Restore Default Wordbank to undo.
Method B: Edit Default File (permanent replacement, good for sharing)
Edit the words array in data/ket.js or data/toefl.js following the same field structure.
Save and reopen index.html to apply changes.
Progress Backup / Device Migration
Progress is stored locally in your browser. Before switching computers or clearing cache, go to Settings → Progress Backup to export progress​ (JSON), then import​ on the new device.
You can also export uploaded wordbanks from the Wordbank page.
File Structure
word-memory-tool/
├─ index.html        # Entry point
├─ style.css         # Styles (kid-friendly color scheme)
├─ app.js            # All logic (scheduling / spelling / progress)
├─ data/
│  ├─ ket.js         # KET/PET default wordbank (editable)
│  └─ toefl.js       # TOEFL default wordbank (editable)
└─ README.md
Tips
In Settings, adjust New Word Count / Daily Total / Seconds per Word, and whether to cloze-test within English sentences.
When a child is tired, doing fewer words is fine — the system auto-defers unfinished words without data loss.
