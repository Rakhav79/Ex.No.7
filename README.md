# Exno.7-Develop a Daily based lovable app using proper prompt based application

# Date:23-10-2025
# Register no.212222070019
# Aim: To develop a daily based lovable app

import React, { useEffect, useMemo, useState } from "react";
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
