# Exno.7-Develop a Daily based lovable app using proper prompt based application

# Date:23-10-2025
# Register no.212222070019
# Aim: To develop a daily based lovable app



import React, { useEffect, useMemo, useState } from "react";

const SAMPLE_PROMPTS = [
  {
    id: "self-1",
    category: "Self-Love",
    tone: "gentle",
    title: "A Letter to You",
    affirmation: "I am worthy of my own care.",
    reflection: "Write a short, compassionate letter to yourself about one thing you did well this week.",
    challenge: "Take 5 minutes today to breathe deeply and place a hand over your heart.",
  },
  {
    id: "self-2",
    category: "Self-Love",
    tone: "minimal",
    title: "Tiny Wins",
    affirmation: "Small steps are progress.",
    reflection: "List three small things you accomplished recently — no matter how small.",
    challenge: "Celebrate one of those wins out loud.",
  },
  {
    id: "mind-1",
    category: "Mindfulness",
    tone: "gentle",
    title: "Five Senses Check-in",
    affirmation: "I am present with the world around me.",
    reflection: "Name one thing you can see, four things you can feel, three things you can hear, two things you can smell, one thing you can taste.",
    challenge: "Do this check-in right now, slowly.",
  },
  {
    id: "love-1",
    category: "Connection",
    tone: "gentle",
    title: "Share a Moment",
    affirmation: "Sharing brings us closer.",
    reflection: "Who made your day better recently? Tell them why (text, voice note, or in person).",
    challenge: "Send a short message of appreciation to one person.",
  },
  {
    id: "love-2",
    category: "Connection",
    tone: "minimal",
    title: "Ask and Listen",
    affirmation: "Curiosity opens the heart.",
    reflection: "Ask someone a question you’ve never asked them and listen without interrupting.",
    challenge: "Schedule 15 minutes for a real conversation this week.",
  },
];

function todaysSeedIndex(total) {
  // deterministic index for today's date
  const d = new Date();
  const key = `${d.getFullYear()}-${d.getMonth() + 1}-${d.getDate()}`;
  let sum = 0;
  for (let i = 0; i < key.length; i++) sum += key.charCodeAt(i);
  return sum % total;
}

export default function DailyLovableGuide() {
  const [prompts, setPrompts] = useState(() => {
    // start with sample prompts; in a real app allow import or cloud sync
    return SAMPLE_PROMPTS;
  });

  const [tone, setTone] = useState(() => {
    return localStorage.getItem("dlg_tone") || "gentle";
  });

  const [overrideIndex, setOverrideIndex] = useState(() => {
    const raw = localStorage.getItem("dlg_override");
    return raw ? Number(raw) : null;
  });

  const [favorites, setFavorites] = useState(() => {
    try {
      return JSON.parse(localStorage.getItem("dlg_favs") || "[]");
    } catch (e) {
      return [];
    }
  });

  const [history, setHistory] = useState(() => {
    try {
      return JSON.parse(localStorage.getItem("dlg_history") || "[]");
    } catch (e) {
      return [];
    }
  });

  const [showSettings, setShowSettings] = useState(false);
  const [notifyAllowed, setNotifyAllowed] = useState(false);

  useEffect(() => {
    localStorage.setItem("dlg_tone", tone);
  }, [tone]);

  useEffect(() => {
    if (overrideIndex !== null) localStorage.setItem("dlg_override", String(overrideIndex));
    else localStorage.removeItem("dlg_override");
  }, [overrideIndex]);

  useEffect(() => {
    localStorage.setItem("dlg_favs", JSON.stringify(favorites));
  }, [favorites]);

  useEffect(() => {
    localStorage.setItem("dlg_history", JSON.stringify(history));
  }, [history]);

  // compute today's prompt list (filter by tone if set)
  const filtered = useMemo(() => prompts.filter((p) => !tone || p.tone === tone), [prompts, tone]);

  const todayIndex = useMemo(() => {
    if (overrideIndex !== null && overrideIndex >= 0 && overrideIndex < filtered.length) return overrideIndex;
    return todaysSeedIndex(filtered.length);
  }, [filtered, overrideIndex]);

  const todayPrompt = filtered[todayIndex];

  function toggleFavorite(id) {
    setFavorites((s) => (s.includes(id) ? s.filter((x) => x !== id) : [...s, id]));
  }

  function markDone(prompt) {
    const entry = { id: prompt.id, title: prompt.title, date: new Date().toISOString() };
    setHistory((h) => [entry, ...h].slice(0, 200));
  }

  // Notifications: request permission and schedule a reminder (works while page open)
  function requestNotificationPermission() {
    if (!("Notification" in window)) return alert("This browser does not support notifications.");
    Notification.requestPermission().then((perm) => {
      setNotifyAllowed(perm === "granted");
      if (perm === "granted") scheduleDailyNotification();
    });
  }

  function scheduleDailyNotification() {
    // schedule a simple notification after 10 seconds for demo and then every 24h while open
    if (!notifyAllowed && Notification.permission !== "granted") return;
    const fire = () => {
      new Notification("Daily Lovable Guide", {
        body: todayPrompt ? `${todayPrompt.title} — ${todayPrompt.affirmation}` : "Your daily prompt is ready.",
        silent: false,
      });
    };
    // for demo: fire in 10s
    setTimeout(fire, 10 * 1000);
    // and schedule a repeating interval while the tab is open
    setInterval(() => {
      fire();
    }, 24 * 60 * 60 * 1000);
  }

  useEffect(() => {
    setNotifyAllowed(Notification && Notification.permission === "granted");
  }, []);

  // UI small helpers
  const isFav = (id) => favorites.includes(id);

  return (
    <div className="min-h-screen bg-gradient-to-b from-rose-50 to-white p-6 flex items-start justify-center">
      <div className="w-full max-w-2xl">
        <header className="flex items-center justify-between mb-6">
          <div>
            <h1 className="text-3xl font-extrabold leading-tight">Daily Lovable Guide</h1>
            <p className="text-sm text-gray-600">Daily prompts, gentle challenges & tiny rituals</p>
          </div>
          <div className="flex items-center gap-2">
            <button
              onClick={() => setShowSettings((s) => !s)}
              className="px-3 py-1 rounded-2xl border shadow-sm text-sm"
            >
              Settings
            </button>
            <button
              onClick={requestNotificationPermission}
              className="px-3 py-1 rounded-2xl bg-rose-500 text-white text-sm shadow"
            >
              Notify
            </button>
          </div>
        </header>

        {showSettings && (
          <div className="bg-white p-4 rounded-2xl shadow mb-6">
            <h3 className="font-semibold mb-2">Appearance & Tone</h3>
            <div className="flex gap-2">
              <button
                onClick={() => setTone("gentle")}
                className={`px-3 py-1 rounded-2xl border ${tone === "gentle" ? "bg-rose-100" : "bg-white"}`}
              >
                Gentle
              </button>
              <button
                onClick={() => setTone("minimal")}
                className={`px-3 py-1 rounded-2xl border ${tone === "minimal" ? "bg-rose-100" : "bg-white"}`}
              >
                Minimal
              </button>
            </div>

            <hr className="my-4" />

            <h3 className="font-semibold mb-2">Prompt Controls</h3>
            <div className="flex gap-2">
              <button
                onClick={() => setOverrideIndex((i) => (i === null ? 0 : Math.max(0, (i + 1) % filtered.length)))}
                className="px-3 py-1 rounded-2xl border"
              >
                Next Prompt
              </button>
              <button onClick={() => setOverrideIndex(null)} className="px-3 py-1 rounded-2xl border">
                Use Today's Prompt
              </button>
            </div>

            <p className="text-xs text-gray-500 mt-3">Notes: Prompts are stored locally. Import/Sync coming soon.</p>
          </div>
        )}

        <main>
          <div className="bg-white rounded-3xl p-6 shadow">
            <div className="flex items-start justify-between">
              <div>
                <div className="text-xs text-gray-500">Prompt for</div>
                <div className="flex items-baseline gap-2">
                  <h2 className="text-2xl font-bold">{todayPrompt ? todayPrompt.title : "No prompt"}</h2>
                  <span className="text-sm text-gray-500">{todayPrompt ? todayPrompt.category : "—"}</span>
                </div>
                <p className="mt-2 text-gray-700">{todayPrompt ? todayPrompt.reflection : ""}</p>
              </div>
              <div className="flex flex-col items-end gap-2">
                <button
                  onClick={() => toggleFavorite(todayPrompt.id)}
                  className="px-3 py-1 rounded-full border"
                >
                  {isFav(todayPrompt.id) ? "★" : "☆"}
                </button>
                <div className="text-right text-xs text-gray-500">{new Date().toLocaleDateString()}</div>
              </div>
            </div>

            <div className="mt-6 grid grid-cols-1 md:grid-cols-3 gap-4">
              <div className="p-4 rounded-xl border">
                <div className="text-xs text-gray-500">Affirmation</div>
                <div className="mt-2 font-semibold">{todayPrompt ? todayPrompt.affirmation : "—"}</div>
              </div>
              <div className="p-4 rounded-xl border">
                <div className="text-xs text-gray-500">Reflection</div>
                <div className="mt-2">{todayPrompt ? todayPrompt.reflection : "—"}</div>
              </div>
              <div className="p-4 rounded-xl border flex flex-col justify-between">
                <div>
                  <div className="text-xs text-gray-500">Challenge</div>
                  <div className="mt-2">{todayPrompt ? todayPrompt.challenge : "—"}</div>
                </div>
                <div className="mt-4 flex gap-2">
                  <button
                    onClick={() => markDone(todayPrompt)}
                    className="px-3 py-2 rounded-2xl bg-rose-500 text-white text-sm shadow"
                  >
                    Mark done
                  </button>
                  <button
                    onClick={() => navigator.share && navigator.share({ title: todayPrompt.title, text: `${todayPrompt.title} — ${todayPrompt.affirmation}` })}
                    className="px-3 py-2 rounded-2xl border text-sm"
                  >
                    Share
                  </button>
                </div>
              </div>
            </div>

            <div className="mt-6">
              <h3 className="font-semibold">Quick browse</h3>
              <div className="mt-3 grid grid-cols-1 sm:grid-cols-2 gap-3">
                {filtered.slice(0, 6).map((p) => (
                  <div key={p.id} className="p-3 rounded-xl border flex items-start justify-between">
                    <div>
                      <div className="font-medium">{p.title}</div>
                      <div className="text-xs text-gray-500">{p.category}</div>
                    </div>
                    <div className="flex flex-col items-end gap-2">
                      <button onClick={() => toggleFavorite(p.id)} className="px-2 py-1 rounded-full border">
                        {isFav(p.id) ? "★" : "☆"}
                      </button>
                      <button onClick={() => setOverrideIndex(filtered.indexOf(p))} className="px-2 py-1 rounded-2xl border text-xs">
                        Use
                      </button>
                    </div>
                  </div>
                ))}
              </div>
            </div>

            <div className="mt-6">
              <h3 className="font-semibold">Favorites</h3>
              <div className="mt-3 grid grid-cols-1 sm:grid-cols-2 gap-3">
                {favorites.length === 0 && <div className="text-sm text-gray-500">No favorites yet — tap the star to save prompts you love.</div>}
                {favorites.map((id) => {
                  const p = prompts.find((x) => x.id === id) || filtered.find((x) => x.id === id);
                  if (!p) return null;
                  return (
                    <div key={id} className="p-3 rounded-xl border flex items-center justify-between">
                      <div>
                        <div className="font-medium">{p.title}</div>
                        <div className="text-xs text-gray-500">{p.category}</div>
                      </div>
                      <div className="flex gap-2">
                        <button onClick={() => toggleFavorite(id)} className="px-2 py-1 rounded-2xl border text-xs">
                          Remove
                        </button>
                        <button onClick={() => setOverrideIndex(filtered.indexOf(p))} className="px-2 py-1 rounded-2xl border text-xs">
                          Use
                        </button>
                      </div>
                    </div>
                  );
                })}
              </div>
            </div>

            <div className="mt-6">
              <h3 className="font-semibold">History</h3>
              <div className="mt-3 space-y-2 text-sm text-gray-600">
                {history.length === 0 && <div className="text-xs text-gray-500">No history yet — mark prompts as done to build your streak.</div>}
                {history.map((h) => (
                  <div key={h.date} className="flex items-center justify-between bg-rose-50 p-2 rounded-md">
                    <div>
                      <div className="font-medium">{h.title}</div>
                      <div className="text-xs text-gray-500">{new Date(h.date).toLocaleString()}</div>
                    </div>
                    <div className="text-xs text-gray-500">✔</div>
                  </div>
                ))}
              </div>
            </div>

            <footer className="mt-6 text-center text-xs text-gray-400">Made with care — Daily Lovable Guide • Prototype</footer>
          </div>
        </main>
      </div>
    </div>
  );
}

